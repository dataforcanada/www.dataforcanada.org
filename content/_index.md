---
title: Welcome to Data for Canada
toc: false
---

## Mission

Data for Canada exists to bridge the gap between open data availability, resiliency, and usability. We curate, clean, and re-engineer high-value Canadian datasets into high-performance, analysis-ready formats for data engineers, researchers/scientists, developers, and systems.

## The Problem

Canada creates incredible amounts of open data, from foundational road networks to federal census statistics and orthoimagery. However, these datasets are often locked in legacy formats, fragmented portals, or structures that require significant engineering effort to normalize. For our target audience, the "time-to-insight" is often bottlenecked by data preparation.

## What Guides Us

We prioritize our work in a utilitarian manner, aiming to provide the greatest amount of good to the greatest amount of individuals. Our approach is guided by the principles of **digital preservation** and the need to keep public information accessible over the long term.

Our approach is guided by the following:

* [Link rot in LIS literature: a 20-year study of web citation decay, recovery and preservation challenges](https://doi.org/10.1108/AJIM-05-2025-0286)
* [Guidance on assessing readiness to manage data according to Findable, Accessible, Interoperable, Reusable (FAIR) principles](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/information-management/guidance-assessing-readiness-manage-data-according-findable-accessible-interoperable-reusable-principles.html)
* [GC White Paper: Data Sovereignty and Public Cloud](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/cloud-services/digital-sovereignty/gc-white-paper-data-sovereignty-public-cloud.html)
* [Sustainability of Digital Formats: Planning for Library of Congress Collections](https://www.loc.gov/preservation/digital/formats/index.html)
* [Cloud-Optimized Geospatial Formats Guide](https://guide.cloudnativegeo.org/)

**Data Stability:**
Beyond technical barriers, open data can be ephemeral. Links break, portals are reorganized, and priorities shift, causing valuable datasets to vanish from the public web. This instability makes it risky to build long-term research or software on top of data providers.

## The Solution

We act as the transformation layer. We aggregate datasets with permissive licenses and process them into "digestible" standards optimized for modern downstream applications.

* **For Data Engineers, Researchers/Scientists, and Developers:** Skip the cleaning phase. Access normalized, documented data ready for analysis.
* **For Systems:** Standardized data structures designed to feed directly into pipelines, data warehouses, and downstream services.

**Our Stewardship:**
Data for Canada takes ownership of the datasets we create, from start to finish. We ensure that data remains consistent and available, acting as a stable foundation for your work, and allowing for reliable analysis across **time and space**. By decoupling access from the original source, we ensure your pipelines don't break even if the upstream location changes or expires.

## Target Software Ecosystem

We adopt an **open-source first** approach, while supporting proprietary solutions to the best of our ability to ensure maximum accessibility. **We target the latest versions of these software packages** (e.g., modern GDAL/OGR) to leverage the newest improvements.

Our data is optimized for:

* **Core Libraries & Tools:** [GDAL/OGR](https://gdal.org/), [QGIS](https://qgis.org/), and [QField](https://qfield.org/).
* **Analysis & Database:** [DuckDB](https://duckdb.org/), [SedonaDB](https://sedona.apache.org/sedonadb/latest/).
* **Serving:** [GeoServer](https://geoserver.org/), [Martin](https://martin.maplibre.org/), and [ZOO-Project](https://zoo-project.org/).
* **Serverless:** [Cloudflare Workers](https://workers.cloudflare.com/), [AWS Lambda](https://aws.amazon.com/lambda/), and [Google Cloud Run functions](https://cloud.google.com/functions).
* **Enterprise:** Esri based products ([ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview), [ArcGIS Server](https://enterprise.arcgis.com/)).

## Explore Sample Datasets

See our processing pipeline in action. View samples and documentation for our current priority processes:

* [**Statistical Products**](https://www.dataforcanada.org/docs/processes/statistical_products/): Census data and other quantitative datasets.
* [**Foundation**](https://www.dataforcanada.org/docs/processes/foundation/#download-and-preview/): Core geospatial layers including address point, road networks, and buildings.
* [**Orthoimagery**](https://www.dataforcanada.org/docs/processes/orthoimagery/#download-and-preview): High-resolution orthoimagery.

## High-Level Overview

**Note:** The data sources in the diagram below are **prioritized from left to right**, reflecting our current focus on processing high-value [statistical](https://www.dataforcanada.org/docs/processes/statistical_products/), [foundational](https://www.dataforcanada.org/docs/processes/foundation/#download-and-preview), and [orthoimagery](https://www.dataforcanada.org/docs/processes/orthoimagery/#download-and-preview) datasets first.

```mermaid
flowchart TD
    classDef linkNode stroke:#0000EE,color:#0000EE,stroke-width:2px;
    subgraph ds [Data Sources]
        Statistical@{ shape: lean-l}
        Foundation@{ shape: lean-l}
        EnvironmentClimate@{ shape: lean-l, label: "Environment, Climate, & Health"}
        Orthoimagery@{ shape: lean-l}
        FieldImagery@{ shape: lean-l, label: "Field Imagery"}
        Elevation@{ shape: lean-l}
        WebCorpus@{ shape: lean-l, label: "Web Corpus"}
    end

    subgraph pp [Processing Pipeline]
        Raw@{ shape: rect, label: "Raw Data Ingestion"}
        Transform@{ shape: rect, label: "Transform and Optimize"}
    end

    subgraph df [Dissemination Formats]
        Parquet@{ shape: lean-l}
        FlatGeoBuf@{ shape: lean-l}
        VectorTiles@{ shape: lean-l, label: "Vector Tiles"}
        NextGenVectorTiles@{ shape: lean-l, label: "Next-Gen Vector Tiles"}
        PMTiles@{ shape: lean-l}
        SQLite@{ shape: lean-l}
        FileGeodatabase@{shape: lean-l, label: "File Geodatabase"}
        GeoTIFF@{ shape: lean-l}
        Zarr@{ shape: lean-l}
        WebP@{ shape: lean-l}
        JPG@{ shape: lean-l}
        PNG@{ shape: lean-l}
        JPEGXL@{ shape: lean-l, label: "JPEG XL"}
        AV1@{ shape: lean-l, label: "AV1"}
        WARC@{ shape: lean-l}
    end

    subgraph di [Distribution Infrastructure]
        ObjectStorage@{ shape: bow-rect, label: "Object Storage"}
        Metadata@{ shape: rect, label: "FAIR Data Catalog"}
        HTTP@{ shape: rect, label: "Static Files"}
        DecentralizedDistribution@{ shape: rect, label: "Decentralized Distribution"}
    end

    subgraph ei [Experimental Infrastructure]
        GeoSpatialServices@{ shape: rect, label: "Geospatial Services"}
        %%Martin@{ shape: rect}
        %%GeoServer@{ shape: rect}
        %%ZOOProject@{ shape: rect, label: "ZOO-Project"}
        %%BBOXServer@{ shape: rect, label: "BBOX Server"}
        %%Panoramax@{ shape: rect}
        %%Pelias@{ shape: rect}
    end

    subgraph "Consumption"
        DataSci@{ shape: rect, label: "Data People & Developers"}
        Systems@{ shape: rect, label: "Systems"}
    end

    %% Relationships
    Statistical a1@--> Raw
    a1@{animate: true, animation: slow}
    Foundation a2@--> Raw
    a2@{animate: true, animation: slow}
    EnvironmentClimate a5@--> Raw
    a5@{animate: true, animation: fast}
    FieldImagery a4@--> Raw
    a4@{animate:true, animation: fast}
    Orthoimagery a3@--> Raw
    a3@{animate: true, animation: slow}
    Elevation a6@--> Raw
    a6@{animate: true, animation: slow}
    WebCorpus a7@--> Raw
    a7@{animate: true, animation: fast}
    Raw a8@--> Transform
    a8@{animate: true, animation: slow}
    Transform a9@--> df
    a9@{animate: true, animation: slow}
    Parquet a10@--> FlatGeoBuf
    a10@{animate: true, animation: fast}
    Parquet a100@--> FileGeodatabase
    Parquet a110@--> SQLite
    a110@{animate: true, animation: slow}
    a100@{animate: true, animation: slow}
    FlatGeoBuf a11@--> VectorTiles
    a11@{animate: true, animation: fast}
    FlatGeoBuf a91@--> NextGenVectorTiles
    a91@{animate: true, animation: fast}
    VectorTiles a90@ --> PMTiles
    a90@{animate: true, animation: fast}
    VectorTiles a96@ --> SQLite
    a96@{animate: true, animation: slow}
    NextGenVectorTiles a92@ --> PMTiles
    a92@{animate: true, animation: slow}
    NextGenVectorTiles a95@ --> SQLite
    a95@{animate: true, animation: slow}
    Zarr a12@ --> WebP
    a12@{animate: true, animation: slow}
    df a13@ --> di
    a13@{animate: true, animation: slow}
    GeoTIFF a14@--> WebP
    a14@{animate: true, animation: slow}
    WebP a93@--> PMTiles 
    a93@{animate: true, animation: slow}
    WebP a94@--> SQLite
    a94@{animate: true, animation: slow}
    WebP a103@--> JPG
    a103@{animate: true, animation: slow}
    WebP a104@--> PNG
    a104@{animate: true, animation: slow}
	JPG a101@--> FileGeodatabase
    a101@{animate: true, animation: slow}
	PNG a102@--> FileGeodatabase
    a102@{animate: true, animation: slow}
    ObjectStorage a15@--> Metadata
    a15@{animate: true, animation: slow}
    Metadata a16@--> HTTP
    a16@{animate: true, animation: slow}
    HTTP a17@--> ei
    a17@{animate: true, animation: slow}
    HTTP a18@--> DecentralizedDistribution
    a18@{animate: true, animation: slow}
    HTTP a19@--> DataSci
    a19@{animate: true, animation: slow}
    DecentralizedDistribution a20@--> Systems
    a20@{animate: true, animation: fast}
    DecentralizedDistribution a21@--> DataSci
    a21@{animate: true, animation: fast}
    Systems a22@ --> DataSci
    a22@{animate: true, animation: fast}
    ei a23@ --> DataSci
    a23@{animate: true, animation: slow}

    %% URLs
    click Foundation "https://github.com/dataforcanada/process-foundation-labs/" _blank
    click Statistical "https://github.com/dataforcanada/process-statistical-labs/" _blank
    click Orthoimagery "https://github.com/dataforcanada/process-orthoimagery-labs/" _blank
    click FieldImagery "https://github.com/dataforcanada/process-field-imagery-labs/" _blank
    click EnvironmentClimate "https://github.com/dataforcanada/process-environmental-climate-health-labs/" _blank
    click Elevation "https://github.com/dataforcanada/process-elevation-labs/" _blank
    click WebCorpus "https://github.com/dataforcanada/process-web-corpus-labs/" _blank

    click Parquet "https://github.com/apache/parquet-format/" _blank
    click FlatGeoBuf "https://flatgeobuf.org/" _blank
    click SQLite "https://www.geopackage.org/" _blank
    click FileGeodatabase "https://gdal.org/en/stable/drivers/vector/openfilegdb.html" _blank
    click VectorTiles "https://github.com/mapbox/vector-tile-spec/" _blank
    click NextGenVectorTiles "https://github.com/maplibre/maplibre-tile-spec/" _blank
    click GeoTIFF "https://cogeo.org/" _blank
    click Zarr "https://github.com/zarr-developers/geozarr-spec/" _blank
    click WebP "https://developers.google.com/speed/webp/" _blank
    click PMTiles "https://github.com/protomaps/PMTiles/blob/main/spec/v3/spec.md" _blank
    click JPEGXL "https://jpeg.org/jpegxl/" _blank
    click AV1 "https://aomedia.org/specifications/av1/" _blank
    click WARC "https://github.com/iipc/warc-specifications/" _blank
    click HTTP "https://www.dataforcanada.org/docs/getting_started/" _blank
    click DecentralizedDistribution "https://www.dataforcanada.org/docs/dissemination/" _blank
    click Metadata "https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/" _blank
    click GeoSpatialServices "https://github.com/dataforcanada/geo-services-labs/" _blank
    click Martin "https://martin.maplibre.org/" _blank
    click GeoServer "https://geoserver.org/" _blank
    click ZOOProject "https://zoo-project.org/" _blank
    click BBOXServer "https://www.bbox.earth/" _blank
    click Panoramax "https://gitlab.com/panoramax" _blank
    click Pelias "https://pelias.io" _blank

    %% APPLY STYLES TO LINKED NODES
    class Foundation,Statistical,Orthoimagery,FieldImagery,EnvironmentClimate,Elevation,WebCorpus linkNode
    class Parquet,FlatGeoBuf,SQLite,FileGeodatabase,VectorTiles,NextGenVectorTiles,GeoTIFF,Zarr,WebP,PMTiles,JPEGXL,AV1,WARC linkNode
    class DecentralizedDistribution,HTTP,Metadata,GeoSpatialServices linkNode
```

## Get Involved

We are actively looking for new members and partners to help shape this project.

### 🇨🇦 Infrastructure Support: Selective Mirroring

To support data sovereignty, safeguard against data loss, and improve local access speeds, **we are currently seeking selective mirroring in Canada**. See our [Infrastructure](/infrastructure).

We are looking for academic institutions, research organizations, or **infrastructure partners** interested in hosting mirrors of specific, high-value dataset subsets. If you have bandwidth and storage capacity to spare for the Canadian open data ecosystem, please [contact us](https://www.dataforcanada.org/contact/).

### Contributing & Feedback

Right now, we primarily need **feedback on our datasets and the underlying processes** used to generate them. If you have thoughts on data quality, format optimization, or pipeline improvements, we want to hear from you.

* **Discussions:** Head over to [#dataforcanada:matrix.org](https://matrix.to/#/#dataforcanada:matrix.org) to chat, or go to the individual process GitHub repos to comment on specific issues.

## License

This project is licensed under the [MIT License](https://opensource.org/license/mit).
