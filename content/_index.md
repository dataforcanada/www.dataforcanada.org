---
title: Welcome to Data for Canada
toc: false
#comments: true
---

## Mission

Data for Canada exists to bridge the gap between open data availability, resiliency, and usability. We curate, clean, and re-engineer high-value Canadian datasets into high-performance, analysis-ready formats for data engineers, researchers/scientists, developers, and systems.

## The Problem

Canada creates incredible amounts of open data, from foundational road networks to federal census statistics and orthoimagery. However, these datasets are often locked in legacy formats, fragmented portals, or structures that require significant engineering effort to normalize. For our target audience, the "time-to-insight" is often bottlenecked by data preparation.

**Data Stability:**
Beyond technical barriers, open data can be ephemeral. Links break, portals are reorganized, and priorities shift, causing valuable datasets to vanish from the public web. This instability makes it risky to build long-term research or software on top of data providers.

## What Guides Us

We prioritize our work in a utilitarian manner, aiming to provide the greatest amount of good to the greatest amount of individuals. Our approach is guided by the principles of **digital preservation** and the need to keep public information accessible over the long term.

Our approach is guided by the following:

* [Link rot in LIS literature: a 20-year study of web citation decay, recovery and preservation challenges](https://doi.org/10.1108/AJIM-05-2025-0286)
* [Guidance on Assessing Readiness to Manage Data According to the Findable, Accessible, Interoperable and Reusable (FAIR) Principles](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/information-management/guidance-assessing-readiness-manage-data-according-findable-accessible-interoperable-reusable-principles.html)
* [Sustainability of Digital Formats: Planning for Library of Congress Collections](https://www.loc.gov/preservation/digital/formats/index.html)
* [Science Needs a Social Network for Sharing Big Data](https://hackmd.io/wKKm4cIDR6a9kYwZ3srVFg?view)
* [Cloud-Optimized Geospatial Formats Guide](https://guide.cloudnativegeo.org/)
* [GC White Paper: Data Sovereignty and Public Cloud](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/cloud-services/digital-sovereignty/gc-white-paper-data-sovereignty-public-cloud.html)

## The Solution

We act as the transformation layer. We aggregate datasets with permissive licenses and process them into "digestible" standards optimized for modern downstream applications.

* **For Data Engineers, Researchers/Scientists, and Developers (AKA Data People):** Skip the cleaning phase. Access normalized, documented data ready for analysis.
* **For Systems:** Standardized data structures designed to feed directly into pipelines, data warehouses, and downstream services.

**Our Stewardship:**
Data for Canada takes ownership of the datasets we create, from start to finish. We ensure that data remains consistent and available, acting as a stable foundation for your work, and allowing for reliable analysis across **time and space**. By decoupling access from the original source, we ensure your pipelines don't break even if the upstream location changes or expires.

## Target Software Ecosystem

We adopt an **open-source first** approach, while supporting proprietary solutions to the best of our ability to ensure maximum accessibility. **We target the latest versions of these software packages** (e.g., modern GDAL/OGR) to leverage the newest improvements.

Our data is optimized for:

| Category | Recommended Stack & Libraries |
| :--- | :--- |
| **Core & Desktop** | [GDAL/OGR](https://gdal.org/), [QGIS](https://qgis.org/), [QField](https://qfield.org/) |
| **Python & Data** | [GeoPandas](https://geopandas.org/), [Lonboard](https://developmentseed.org/lonboard/latest/), [DuckDB](https://duckdb.org/), [SedonaDB](https://sedona.apache.org/sedonadb/latest/)|
| **Database** | [PostgreSQL](https://www.postgresql.org/) with [PostGIS](https://postgis.net/) and [pg_mooncake](https://www.mooncake.dev/pgmooncake/) extensions |
| **Serving** | [GeoServer](https://geoserver.org/), [Martin](https://martin.maplibre.org/), [ZOO-Project](https://zoo-project.org/) |
| **Serverless** | [Cloudflare Workers](https://workers.cloudflare.com/), [AWS Lambda](https://aws.amazon.com/lambda/), [Google Cloud Run functions](https://cloud.google.com/functions) |
| **Enterprise** | [ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview), [ArcGIS Enterprise](https://enterprise.arcgis.com/) |

## Explore Sample Datasets

See our processing pipeline in action. View samples and documentation for our current priority data packages (AKA `d4c-pkgs`):

* [**Statistical Products**](https://www.dataforcanada.org/docs/d4c-pkgs/d4c-datapkg-statistical/): Census data and other quantitative datasets.
* [**Foundation**](https://www.dataforcanada.org/docs/d4c-pkgs/d4c-datapkg-foundation/#download-and-preview/): Core geospatial layers including address point, road networks, and buildings.
* [**Orthoimagery**](https://www.dataforcanada.org/docs/d4c-pkgs/d4c-datapkg-orthoimagery/#download-and-preview): High-resolution orthoimagery.

## High-Level Overview

**Note:** The data sources in the diagram below are **prioritized from left to right**, reflecting our current focus on processing high-value [statistical](https://www.dataforcanada.org/docs/d4c-pkgs/d4c-datapkg-statistical/), [foundational](https://www.dataforcanada.org/docs/d4c-pkgs/d4c-datapkg-foundation/#download-and-preview), and [orthoimagery](https://www.dataforcanada.org/docs/d4c-pkgs/d4c-datapkg-orthoimagery/#download-and-preview) datasets first.

{{< rawhtml >}}
<style>
    .inline-svg-container a {
        fill: #0074D9; 
        text-decoration: underline;
        transition: fill 0.2s ease;
    }

    .inline-svg-container a:hover {
        fill: #FF4136;
        cursor: pointer;
    }

    .inline-svg-container svg {
        width: 100%;
        height: auto;
        max-width: 100%;
        background-color: transparent !important;
    }
    
</style>
{{< /rawhtml >}}

<!-- Put back mermaid until I figure it all out -->
{{< svg src="static/high-level-overview-homepage.svg" alt="High Level Overview" >}}

## Get Involved

We are actively looking for members and partners who want to help scale the Canadian open data ecosystem. Whether you represent an institution or are an individual developer, there are several ways to support the mission.

### Infrastructure Support & Global Mirroring

To safeguard against data loss and improve global access speeds, we are seeking **Global Infrastructure Partners** to help host and distribute our datasets.

* **Selective Mirroring:** We are looking for academic institutions, research organizations, or infrastructure partners worldwide interested in hosting mirrors of specific, high-value dataset subsets (e.g., Census, foundation, and orthoimagery data).
* **Build Infrastructure:** We are seeking partners to host our **build and ETL infrastructure**. If you have available compute resources (High-CPU/RAM instances or specialized CI/CD runners) to help accelerate our data transformation layer, please [contact us](https://www.dataforcanada.org/contact/).

### Contributing & Feedback

We welcome any type of feedback—from bug reports in our transformation logic to suggestions on data schema improvements. For technical feedback or to contribute to specific data pipelines, please visit the relevant repositories:

* **[d4c-datapkg-statistical](https://github.com/dataforcanada/d4c-datapkg-statistical)**
* **[d4c-datapkg-foundation](https://github.com/dataforcanada/d4c-datapkg-foundation)**
* **[d4c-datapkg-orthoimagery](https://github.com/dataforcanada/d4c-datapkg-orthoimagery)**

Join the conversation at [#dataforcanada:matrix.org](https://matrix.to/#/#dataforcanada:matrix.org) to chat, or provide feedback directly on the GitHub repositories listed above.

## License

This project is licensed under the [MIT License](https://opensource.org/license/mit).
