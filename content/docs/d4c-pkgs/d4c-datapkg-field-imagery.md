---
title: Field Imagery
weight: 4
next: /docs/d4c-infra-distribution/
---

## The Mission

Commercial street-level imagery is often locked behind restrictive licenses, proprietary viewers, and paywalls, making it inaccessible to our target audience. We are building a sovereign, open-source alternative for Canada.

We will be using **[Panoramax](https://panoramax.fr/)** as a base, but will be expanding upon the project to provide a decentralized platform where field imagery is treated as a public utility: fully downloadable, API-accessible, privacy-compliant, and resilient to shifting priorities.

## The Infrastructure

* **Storage**: High-performance object storage backend for hosting terabytes of 360°, flat field imagery, and oblique imagery.

## The Processing Pipeline

We treat field imagery as a data engineering challenge, ensuring "time-to-insight" is minimized for downstream users.

1. **Ingestion**: Raw imagery is captured using diverse hardware (ex. 360° cameras, mobile rigs, meta glasses, drones, etc.) and ingested by our systems.
2. **Privacy & Anonymization**: Before publication, all imagery undergoes a rigorous privacy scrub. We utilize automated detection pipelines to blur faces and license plates, ensuring compliance with Canadian privacy standards while maintaining data utility.
3. **Standardization**: Images are processed into systems-ready formats, making it ready for analysis.
4. **Metadata Extraction**: We extract and normalize/strip identifiying information (ex. EXIF and GPS telemetry), indexing it into a **[FAIR Catalogue](https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/)**.

## Data Products

Unlike commercial platforms that only offer a "view" of the data, we provide the **data itself**.

* **Bulk Datasets**: Curated dumps of street-level imagery available for computer vision training, asset management, and change detection models.
* **[FAIR Data Catalogue](https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/) Integration**: Seamless integration with geospatial workflows (ex. DuckDB, QGIS, Python, R, Julia, etc.).
