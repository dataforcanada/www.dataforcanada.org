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
        StatCan[("Statistical Products")]:::source
        Orthoimagery[("Orthoimagery")]:::source
    end

    subgraph "Processing Pipeline"
        Raw[Raw Data Ingestion<br/>CSVs, Shapefiles, ECW]:::process
        Transform[Transformation Engine<br/>Open & Closed Source]:::process
        Opt[Optimization]:::process
    end

    subgraph "Dissemination Formats"
        Parquet[("Parquet Files")]:::storage
        PMTiles[("PMTiles")]:::storage
        FlatGeoBuf[("FlatGeoBuf")]:::storage
    end

    subgraph "Distribution Infrastructure"
        S3_COMPLIANT_STORAGE[S3 Compliant Storage]:::storage
        Decentralized_Distribution[Decentralized Distribution]:::storage
        Serverless[Cloudflare Worker<br/>API & Serving]:::storage
    end

    subgraph "Consumption / End Users"
        DataSci[DuckDB, Python, QGIS, Jupyter]:::consumer
        WebApps[Web Applications]:::consumer
        DataSci[Python]:::consumer
        Systems[Systems]:::consumer
    end

    %% Relationships
    StatCan --> Raw
    Raw --> Transform
    Transform --> Opt
    Opt --> Parquet
    Opt --> PMTiles
    Opt --> FlatGeoBuf
    Parquet --> S3_COMPLIANT_STORAGE
    PMTiles --> S3_COMPLIANT_STORAGE
    FlatGeoBuf --> S3_COMPLIANT_STORAGE
    S3_COMPLIANT_STORAGE --> Decentralized_Distribution
    S3_COMPLIANT_STORAGE --> Serverless
    Decentralized_Distribution --> Systems
    Serverless --> WebApps
    Serverless --> DataSci

    %% Concept Annotations
    Transform -.->|"Join Spatial & Tabular"| Parquet
    PMTiles -.->|"Stream tiles"| WebApps
```
