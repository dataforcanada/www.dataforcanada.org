---
title: Orthoimagery
weight: 3
---

I briefly worked on collecting orthoimagery a couple of years ago. It started from [this](https://github.com/diegoripley/canada-orthoimagery). Current data processing pipeline is being defined, but you can preview some of the datasets from the process.

## Development Environment

While a key goal is to utilize open source as much as possible, We utilize the proprietary software [MapTiler Engine Pro](https://www.maptiler.com/engine/pricing) as it is superior to current open source solutions. A limitation is that we are limited to 8 CPU cores for rendering of the map tiles.

## Specifications of Tile Packages

The specifications for the tile packages are defined in this code.

```bash
#!/bin/bash
PROJECT_DIR="~/Documents/Personal/Projects/dataforcanada-orthoimagery"
DATASET_ID="ca-mb_winnipeg-2024A00054611040_orthoimagery_2024_075mm"
DATA_DIR="${PROJECT_DIR}/data"
DATA_INPUT_DIR="${DATA_DIR}/input/${DATASET_ID}"
DATA_OUTPUT_DIR="${DATA_DIR}/output/${DATASET_ID}"

MBTILES_OUTPUT_FILE="${DATA_OUTPUT_DIR}/${DATASET_ID}.mbtiles"
PMTILES_OUTPUT_FILE="${DATA_OUTPUT_DIR}/${DATASET_ID}.pmtiles"

# Define arguments in an array
ARGS=(
  -progress
  -name "City of Winnipeg Orthoimagery for 2024 / Ortho-imagerie de la Ville de Winnipeg de 2024"
  -description "Orthoimagery 7.5cm resolution. / Ortho-imagerie à résolution de 7,5 cm."
  -attribution "Source: data.winnipeg.ca / Source: data.winnipeg.ca"
  -srs_epsg
  -mbtiles_compatible
  -wo "NUM_THREADS=ALL_CPUS"
  -wo "USE_OPENCL=TRUE"
  -sparse
  -scale 2.000000
  -work_dir ~/tmp/maptiler_engine
  -f webp32
  -webp_quality 85
  -webp_lossy
  -webp_preset photo
  -resampling cubic
  -overviews_resampling average
  -o "${MBTILES_OUTPUT_FILE}"
  $DATA_INPUT_DIR/*.ecw
)

# Run the command with the array
maptiler-engine "${ARGS[@]}"

pmtiles convert --tmpdir=~/tmp/pmtiles ${MBTILES_OUTPUT_FILE} ${PMTILES_OUTPUT_FILE}
```

## Download and Preview

Here is a table of some of the datasets created from the current process.

| Place      | ISO | Province | Year | Provider   | Dataset ID / Preview                                                | PMTiles                                                                                                            | TileJSON                                                                                                         |
|------------|-----|----------|------|------------|------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| Canada     | CA  |          | 2020 | NRCan      | [ca_nrcan_land_cover_2020_30m](https://data-01.dev.dataforcanada.org/processed/ca_nrcan_land_cover_2020_30m.html)                               | <https://data-01.dev.dataforcanada.org/processed/ca_nrcan_land_cover_2020_30m.pmtiles>                               | <https://tiles-01.dev.dataforcanada.org/processed/ca_nrcan_land_cover_2020_30m.json>                               |
| Edmonton   | CA  | AB       | 2023 | Edmonton   | [ca-ab_edmonton-2023A00054811061_orthoimagery_2023_075mm](https://data-01.dev.dataforcanada.org/processed/ca-ab_edmonton-2023A00054811061_orthoimagery_2023_075mm.html)    | <https://data-01.dev.dataforcanada.org/processed/ca-ab_edmonton-2023A00054811061_orthoimagery_2023_075mm.pmtiles>    | <https://tiles-01.dev.dataforcanada.org/processed/ca-ab_edmonton-2023A00054811061_orthoimagery_2023_075mm.json>    |
| Red Deer   | CA  | AB       | 2024 | Red Deer   | [ca-ab_red_deer-2024A00054808011_orthoimagery_2024_075mm](https://data-01.dev.dataforcanada.org/processed/ca-ab_red_deer-2024A00054808011_orthoimagery_2024_075mm.html)    | <https://data-01.dev.dataforcanada.org/processed/ca-ab_red_deer-2024A00054808011_orthoimagery_2024_075mm.pmtiles>    | <https://tiles-01.dev.dataforcanada.org/processed/ca-ab_red_deer-2024A00054808011_orthoimagery_2024_075mm.json>    |
| Vancouver  | CA  | BC       | 2022 | Vancouver  | [ca-bc_vancouver-2022A00055915022_orthoimagery_2022_075mm](https://data-01.dev.dataforcanada.org/processed/ca-bc_vancouver-2022A00055915022_orthoimagery_2022_075mm.html)   | <https://data-01.dev.dataforcanada.org/processed/ca-bc_vancouver-2022A00055915022_orthoimagery_2022_075mm.pmtiles>   | <https://tiles-01.dev.dataforcanada.org/processed/ca-bc_vancouver-2022A00055915022_orthoimagery_2022_075mm.json>   |
| Whitehorse | CA  | YK       | 2019 | Whitehorse | [ca-yt_whitehorse-2019A000556001009_orthoimagery_2019_200mm](https://data-01.dev.dataforcanada.org/processed/ca-bc_vancouver-2022A00055915022_orthoimagery_2022_075mm.html) | <https://data-01.dev.dataforcanada.org/processed/ca-yt_whitehorse-2019A000556001009_orthoimagery_2019_200mm.pmtiles> | <https://tiles-01.dev.dataforcanada.org/processed/ca-yt_whitehorse-2019A000556001009_orthoimagery_2019_200mm.json> |
| Winnipeg   | CA  | MB       | 2024 | Winnipeg   | [ca-mb_winnipeg-2024A00054611040_orthoimagery_2024_075mm](https://data-01.dev.dataforcanada.org/processed/ca-mb_winnipeg-2024A00054611040_orthoimagery_2024_075mm.html)    | <https://data-01.dev.dataforcanada.org/processed/ca-mb_winnipeg-2024A00054611040_orthoimagery_2024_075mm.pmtiles>    | <https://tiles-01.dev.dataforcanada.org/processed/ca-mb_winnipeg-2024A00054611040_orthoimagery_2024_075mm.json>    |

## The Plan

The plan is to include the original dataset, for example, the orthoimagery files from [Vancouver](https://opendata.vancouver.ca/explore/dataset/orthophoto-imagery-2022/information/) are provided in MrSID and ECW file formats, which are proprietary and require special drivers being used. I am looking into using formats such as [Cloud Optimized GeoTIFFs](https://cogeo.org/), but I have to make sure that there is no degradation of visual quality in the process. I hope to experiment with multispectral data in the future.
