---
title: Census Data
weight: 2
next: /docs/processes/orthoimagery/
---

Look through our [process-statcan-data-labs](https://github.com/dataforcanada/process-statcan-data-labs) repo for the datasets processed. There is still lots of work to do to make it ready for systems.

## Download

Below is a table of datasets generated from our current processing pipeline. You can download the raw **Parquet** files directly or use the **Map Preview** links to inspect the data as vector tiles.

### How to use the Map Preview

The map preview allows you to visualize specific census characteristics dynamically. Follow this workflow to verify the data before downloading.

**1. Identify your Characteristic ID**
Census variables are mapped using numeric IDs. Consult the **[Characteristic ID Reference Sheet](https://1drv.ms/x/c/d42308bcd3b7a4a1/ESlrAmKqXp9BnsMXqurcB0sB9qy1r2-ZV8tCL9nCns_Mpg?e=8qIroJ)** to find the ID for the data you want to view.

* *Example:* The ID for "Number of COVID-19 emergency and recovery benefits recipients..." is **124**.

**2. Open the Preview**
Click the link in the **Dataset ID & Preview** column for your desired geographic level (e.g., Provinces, Federal Electoral Districts).

**3. Filter by Attribute**
In the top-right "Search fields" box, enter the attribute key using the format `{gender}_{ID}`:

* **Total:** Enter `total_124`
* **Male:** Enter `men_124`
* **Female:** Enter `women_124`

**4. Update the Map**
Click the **"Recalculate Classes"** button. This will refresh the map legend and choropleth coloring based on the currently visible extent.

{{< callout type="info">}}
**Note on Data Availability:** Dissemination blocks currently only contain these **[4 specific characteristics](https://github.com/dataforcanada/process-statcan-data-labs/issues/6)**.
{{< /callout >}}

{{< callout type="note">}}
**Credit:**

* The location search functionality in our map previews is powered by the **[PHAC Geocoder](https://geocoder.alpha.phac.gc.ca/)**.
* The basemaps is generously served through [OpenFreeMap](https://openfreemap.org/).
{{< /callout >}}

| Place  | ISO | Date | Provider | Dataset ID & Preview                                                                                                                                                                                               | Parquet                                                                                                                                                       | PMTiles **(draft)**                                                                                                                      |
| ------ | --- | ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_provinces_territories_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/pr/#3.08/58.69/-99.19)                                             | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_provinces_territories_tabular_2021.parquet)                                 | [Download](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/pr/pr_2021_cop.pmtiles)                  |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_federal_electoral_districts_2013_representation_order_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/fed_2021_2013/#6.6/44.319/-78.272) | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_federal_electoral_districts_2013_representation_order_tabular_2021.parquet) | [Download](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/fed_2021_2013/fed_2021_2013_cop.pmtiles) |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_federal_electoral_districts_2023_representation_order_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/fed_2021_2023/#6.6/44.319/-78.272) | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_federal_electoral_districts_2023_representation_order_tabular_2021.parquet) | [Download](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/fed_2021_2023/fed_2021_2023_cop.pmtiles) |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_economic_regions_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/er/#6/45.425/-75.695)                                                   | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_economic_regions_tabular_2021.parquet)                                      | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/er/er_2021_cop.pmtiles)                   |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_census_metropolitan_areas_and_census_agglomerations_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/cma/#4/45.42/-75.69)                 | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_census_metropolitan_areas_and_census_agglomerations_tabular_2021.parquet)   | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/cma/cma_2021_cop.pmtiles)                 |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_census_divisions_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/cd/#8/45.425/-75.695)                                                   | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_census_divisions_tabular_2021.parquet)                                      | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/cd/cd_2021_cop.pmtiles)                   |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_designated_places_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/dpl/#8/43.606/-80.328)                                                 | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_designated_places_tabular_2021.parquet)                                     | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/dpl/dpl_2021_cop.pmtiles)                 |
| Canada | CA  | 2021 | StatCan  | ca_statcan_census_pop_census_consolidated_subdivisions_tabular_2021                                                                                                                                                |                                                                                                                                                               |                                                                                                                                          |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_aggregate_dissemination_areas_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/ada/#10/45.4247/-75.695)                                   | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_aggregate_dissemination_areas_tabular_2021.parquet)                         | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/ada/ada_2021_cop.pmtiles)                 |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_census_subdivisions_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/cd/#8/45.425/-75.695)                                                | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_census_subdivisions_tabular_2021.parquet)                                   | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/csd/csd_2021_cop.pmtiles)                 |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_designated_places_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/dpl/#8/43.606/-80.328)                                                 | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_designated_places_tabular_2021.parquet)                                     | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/dpl/dpl_2021_cop.pmtiles)                 |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_population_centres_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/pop_ctr/#4/45.42/-75.69)                                              | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_population_centres_tabular_2021.parquet)                                    | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/pop_ctr/pop_ctr_2021_cop.pmtiles)         |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_forward_sortation_areas_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/fsa/#10/45.4247/-75.695)                                         | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_forward_sortation_areas_tabular_2021.parquet)                               | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/fsa/fsa_2021_cop.pmtiles)                 |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_census_tracts_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/ct/#12/45.40309/-75.70183)                                                 | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_census_tracts_tabular_2021.parquet)                                         | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/ct/ct_2021_cop.pmtiles)                   |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_dissemination_areas_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/da/#10/45.4247/-75.695)                                              | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_dissemination_areas_tabular_2021.parquet)                                   | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/da/da_2021_cop.pmtiles)                   |
| Canada | CA  | 2021 | StatCan  | [ca_statcan_census_pop_dissemination_blocks_tabular_2021](https://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/db/#10/45.4247/-75.695)                                             | [Download](https://data-01.labs.dataforcanada.org/processed/ca_statcan_census_pop_dissemination_blocks_tabular_2021.parquet)                                  | [Download](http://data-01.diegoripley.ca/census_of_population_2021_vector_tiles_august_12_2025/db/db_2021_cop.pmtiles)                   |
