---
title: Welcome to Data for Canada
toc: false
---

## Mission

Data for Canada exists to bridge the gap between open data availability and data usability. We curate, clean, and re-engineer high-value Canadian datasets into high-performance, analysis-ready formats for researchers, developers, and systems.

## The Problem

Canada creates incredible amounts of open data, from foundational road networks to federal census statistics. However, these datasets are often locked in legacy formats, fragmented portals, or structures that require significant engineering effort to normalize before they can be used. For a researcher or a system developer, the "time-to-insight" is often bottlenecked by data preparation.

## The Solution

We act as the transformation layer. We aggregate datasets with permissive licenses and process them into "digestible" standards optimized for modern downstream applications.

* **For Researchers:** Skip the cleaning phase. Access normalized, documented data ready for analysis.
* **For Systems:** Standardized data structures designed to feed directly into pipelines, data warehouses, and downstream services.

## High-Level Overview

```mermaid
flowchart TD
    %% Define Styles
    classDef source fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef process fill:#fff9c4,stroke:#fbc02d,stroke-width:2px
    classDef storage fill:#e0f2f1,stroke:#00695c,stroke-width:2px
    classDef consumer fill:#f3e5f5,stroke:#8e24aa,stroke-width:2px

    subgraph "Data Sources"
        StatProducts[("Statistical Products")]:::source
        Orthoimagery[("Orthoimagery")]:::source
    end

    subgraph "Processing Pipeline"
        Raw[Raw Data Ingestion<br/>CSVs, Shapefiles, ECW]:::process
        Transform[Transformation Engine]:::process
        Opt[Optimization]:::process
    end

    subgraph "Dissemination Formats"
        Parquet[("Parquet")]:::storage
        FlatGeoBuf[("FlatGeoBuf")]:::storage
        PMTiles[("PMTile")]:::storage
        COG[("COG")]:::storage
    end

    subgraph "Distribution Infrastructure"
        ObjectStorage[Object Storage]:::storage
        DecentralizedDistribution[Decentralized Distribution]:::storage
        Serverless[API & Static Files]:::storage
        Metadata[Metadata]:::storage
    end

    subgraph "Experimental Infrastructure"
        GeoServer
        QGISServer[("QGIS Server")]
        Martin
    end

    subgraph "Consumption / End Users"
        DataSci[DuckDB, Python, QGIS, Jupyter]:::consumer
        WebApps[Web Applications]:::consumer
        DataSci[Python, R, Julia]:::consumer
        Systems[Systems]:::consumer
    end

    %% Relationships
    StatProducts --> Raw
    Raw --> Transform
    Transform --> Opt
    Opt --> Parquet
    Opt --> FlatGeoBuf
    Opt --> PMTiles
    Opt --> COG
    Parquet --> ObjectStorage
    FlatGeoBuf --> ObjectStorage
    PMTiles --> ObjectStorage
    COG --> ObjectStorage
    ObjectStorage --> Metadata
    Metadata --> DecentralizedDistribution
    Metadata --> Serverless
    Metadata --> GeoServer
    Metadata --> QGISServer
    Metadata --> Martin
    Metadata --> DataSci
    Metadata --> WebApps
    Metadata --> Systems
    DecentralizedDistribution --> Systems
    Serverless --> WebApps
    Serverless --> DataSci
    ObjectStorage --> GeoServer
    ObjectStorage --> QGISServer
    ObjectStorage --> Martin
    GeoServer --> WebApps
    QGISServer --> WebApps
    Martin --> WebApps
    GeoServer --> DataSci
    QGISServer --> DataSci
    Martin --> DataSci

    click Parquet "https://github.com/apache/parquet-format" _blank
    click FlatGeoBuf "https://flatgeobuf.org" _blank
    click PMTiles "https://github.com/protomaps/PMTiles/blob/main/spec/v3/spec.md" _blank
    click StatProducts "https://www.dataforcanada.org/docs/processes/statistical_products/" _blank
    click Orthoimagery "https://www.dataforcanada.org/docs/processes/orthoimagery/" _blank
    click DecentralizedDistribution "https://www.dataforcanada.org/docs/dissemination/" _blank
    click Metadata "https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/" _blank
    click Martin "https://martin.maplibre.org/" _blank
    click GeoServer "https://geoserver.org/" _blank
    click COG "https://cogeo.org/" _blank
```
