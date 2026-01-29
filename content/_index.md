---
title: Welcome to Data for Canada
toc: false
---

## Mission

Data for Canada exists to bridge the gap between open data availability and data usability. We curate, clean, and re-engineer high-value Canadian datasets into high-performance, analysis-ready formats for researchers, developers, and systems.

## The Problem

Canada creates incredible amounts of open data, from foundational road networks, federal census statistics, orthoimagery, and other. However, these datasets are often locked in legacy formats, fragmented portals, or structures that require significant engineering effort to normalize before they can be used. For a researcher or a system developer, the "time-to-insight" is often bottlenecked by data preparation.

## The Solution

We act as the transformation layer. We aggregate datasets with permissive licenses and process them into "digestible" standards optimized for modern downstream applications.

* **For Researchers and Developers:** Skip the cleaning phase. Access normalized, documented data ready for analysis.
* **For Systems:** Standardized data structures designed to feed directly into pipelines, data warehouses, and downstream services.

## High-Level Overview

```mermaid
flowchart TD
    subgraph ds [Data Sources]
        StatProducts@{ shape: lean-l, label: "Statistical Products"}
        Orthoimagery@{ shape: lean-l}
        FieldImagery@{ shape: lean-l, label: "Field Imagery"}
        Elevation@{ shape: lean-l}
        EnvironmentClimate@{ shape: lean-l, label: "Environmental & Climate"}
    end

    subgraph pp [Processing Pipeline]
        Raw@{ shape: rect, label: "Raw Data Ingestion"}
        Transform@{ shape: rect, label: "Transform and Optimize"}
    end

    subgraph df [Dissemination Formats]
        Parquet@{ shape: lean-l}
        FlatGeoBuf@{ shape: lean-l}
        PMTiles@{ shape: lean-l}
        COG@{ shape: lean-l}
        Zarr@{ shape: lean-l}
        JPEGXL@{ shape: lean-l, label: "JPEG XL"}
        AV1@{ shape: lean-l, label: "AV1"}
    end

    subgraph di [Distribution Infrastructure]
        ObjectStorage@{ shape: bow-rect, label: "Object Storage"}
        Metadata@{ shape: rect}
        HTTP@{ shape: rect, label: "Static Files & API"}
        DecentralizedDistribution@{ shape: rect, label: "Decentralized Distribution"}
    end

    subgraph ei [Experimental Infrastructure]
        Martin@{ shape: rect}
        GeoServer@{ shape: rect}
        ZOOProject@{ shape: rect, label: "ZOO-Project"}
        BBOXServer@{ shape: rect, label: "BBOX Server"}
        Panoramax@{ shape: rect}
    end

    subgraph "Consumption"
        DataSci@{ shape: rect, label: "Researchers & Developers"}
        Systems@{ shape: rect, label: "Systems"}
    end

    %% Relationships
    StatProducts a1@--> Raw
    a1@{animate: true, animation: slow}
    Orthoimagery a2@--> Raw
    a2@{animate: true, animation: slow}
    FieldImagery a32@--> Raw
    a32@{animate:true, animation: fast}
    EnvironmentClimate a31@--> Raw
    a31@{animate: true, animation: fast}
    Elevation a3@--> Raw
    a3@{animate: true, animation: slow}
    Raw a4@--> Transform
    a4@{animate: true, animation: slow}
    Transform a5@--> df
    a5@{animate: true, animation: slow}
    Parquet a7@--> FlatGeoBuf
    a7@{animate: true, animation: slow}
    Parquet a8@--> PMTiles
    a8@{animate: true, animation: slow}
    Zarr a39@ --> PMTiles
    a39@{animate: true, animation: slow}
    df a36@ --> di
    a36@{animate: true, animation: slow}
    COG a28@--> PMTiles
    a28@{animate: true, animation: slow}
    ObjectStorage a14@--> Metadata
    a14@{animate: true, animation: slow}
    Metadata a15@--> HTTP
    a15@{animate: true, animation: slow}
    HTTP a16@--> ei
    a16@{animate: true, animation: slow}
    HTTP a17@--> DecentralizedDistribution
    a17@{animate: true, animation: slow}
    HTTP a18@--> DataSci
    a18@{animate: true, animation: slow}
    DecentralizedDistribution a22@--> Systems
    a22@{animate: true, animation: fast}
    DecentralizedDistribution a23@--> DataSci
    a23@{animate: true, animation: fast}
    Systems a38@ --> DataSci
    a38@{animate: true, animation: fast}

    ei a40@ --> DataSci
    a40@{animate: true, animation: slow}

    click Parquet "https://github.com/apache/parquet-format/" _blank
    click FlatGeoBuf "https://flatgeobuf.org/" _blank
    click PMTiles "https://github.com/protomaps/PMTiles/blob/main/spec/v3/spec.md" _blank
    click Zarr "https://github.com/zarr-developers/geozarr-spec/" _blank
    click StatProducts "/docs/processes/statistical_products/" _blank
    click Orthoimagery "/docs/processes/orthoimagery/" _blank
    %%click FieldImagery "/docs/processes/field_imagery/" _blank
    %%click EnvironmentClimate "/docs/processes/environmental_climate/" _blank
    %%click Elevation "/docs/processes/elevation/" _blank
    click JPEGXL "https://jpeg.org/jpegxl/" _blank
    click AV1 "https://aomedia.org/specifications/av1/" _blank
    click DecentralizedDistribution "/docs/dissemination/" _blank
    click Metadata "https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/" _blank
    click Martin "https://martin.maplibre.org/" _blank
    click GeoServer "https://geoserver.org/" _blank
    click Panoramax "https://gitlab.com/panoramax" _blank
    click COG "https://cogeo.org/" _blank
    click ZOOProject "https://zoo-project.org/" _blank
    click BBOXServer "https://www.bbox.earth/" _blank
```
