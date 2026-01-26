---
title: "DuckDB"
---

Here is a DuckDB example.

```sql {filename="duckdb_example.sql"}
-- Load Extensions
INSTALL httpfs;
LOAD httpfs;
INSTALL spatial;
LOAD spatial;

-- Verbosity & Performance Monitoring
SET enable_progress_bar=true;
PRAGMA enable_profiling='query_tree';
SET explain_output='all';SET enable_progress_bar=true;
PRAGMA enable_profiling='json'; -- or 'query_tree' for a visual text tree
SET http_keep_alive=true;

-- Save Results to Local Database
ATTACH 'census_data.db' AS census_data_db;

/*

How to Determine the Field Names for Census of Population Characteristics

1. First find the characteristic ID by going to https://1drv.ms/x/c/d42308bcd3b7a4a1/ESlrAmKqXp9BnsMXqurcB0sB9qy1r2-ZV8tCL9nCns_Mpg?e=8qIroJ
2. Construct the field name 
- If we wanted the total count for the "Population, 2021" characteristic, we would search for "count_total_1"
- If we wanted the male count for the "Population, 2021" characteristic, we would search for "count_male_total_1"
- If we wanted the female count for the "Population, 2021" characteristic, we would search for "count_female_total_1"
*/

/*
Get the following 2021 Census characteristics:
   - count_total_1 - "Population, 2021".
   - count_total_4 - "Total private dwellings".
   - count_total_155 - "Total - Total income groups in 2020 for the population aged 15 years and over in private households - 100% data"
   population, total private dwellings, and calculate percentage of population that
   makes $100,000 or more, by Dissemination Area (2021 Census)".
Then we calculate the percentage of private households that earn $100,000 and over:
   - percentage_over_100k - calculated from count_total_4 and count_total_5.
*/
-- Useful to see performance of queries
-- EXPLAIN ANALYZE SELECT
CREATE OR REPLACE TABLE census_data_db.da_income_stats_montreal AS 
WITH calculated_data AS (
    SELECT
        geo.da_dguid,
        geo.csd_dguid,
        cop.count_total_1 AS population_2021,
        cop.count_total_155 AS private_households_with_income,
        cop.count_total_168 AS private_households_over_100k,
        CAST((ST_Area_Spheroid(ST_FlipCoordinates(geo.geom)) / 1000000.0) AS DECIMAL(10, 4)) AS area_km2 -- Area in square kilometers
        ,geo.geom
    FROM
        'https://data-01.dataforcanada.org/processed/ca_statcan_census_pop_dissemination_areas_tabular_2021.parquet' AS cop,
        'https://data-01.dataforcanada.org/processed/ca_statcan_dissemination_areas_digital_2021.parquet' AS geo
    WHERE 
        cop.da_dguid = geo.da_dguid
        AND geo.csd_dguid = '2021A00052466023' -- Montréal, QC
        AND cop.count_total_1 > 0
)
SELECT
    da_dguid,
    csd_dguid,
    population_2021,
    private_households_with_income,
    private_households_over_100k,
    CAST(
        CASE WHEN private_households_with_income > 0 
        THEN (CAST(private_households_over_100k AS BIGINT) * 100.00 / private_households_with_income)
        ELSE 0 END AS DECIMAL(5, 2)
    ) AS private_households_percentage_over_100k,
    CAST(
        CASE WHEN area_km2 > 0 
        THEN (private_households_over_100k / area_km2)
        ELSE 0 END AS INTEGER
    ) AS private_households_over_100k_per_km2
    --
    ,geom
FROM
    calculated_data
ORDER BY 
    private_households_over_100k_per_km2 DESC,
    private_households_percentage_over_100k DESC
;

-- Output as GeoParquet
COPY geo_data TO 'ca_statcan_dissemination_areas_digital_2021_private_dwellings_questions.parquet' (FORMAT PARQUET);
-- Output as File Geodatabase
COPY geo_data TO 'ca_statcan_dissemination_areas_digital_2021_private_dwellings_question.gdb'
WITH (
  FORMAT GDAL,
  DRIVER 'OpenFileGDB',
  GEOMETRY_TYPE 'POLYGON',
  SRS 'EPSG:4326'
);
```