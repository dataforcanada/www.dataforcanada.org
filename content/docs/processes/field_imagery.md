---
title: 📸 Field Imagery
weight: 4
next: /docs/dissemination/
---

## The Mission

Commercial street-level imagery is often locked behind restrictive licenses, proprietary viewers, and paywalls, making it inaccessible to our target audience. We are building a sovereign, open-source alternative for Canada.

By self-hosting a **[Panoramax](https://panoramax.fr/)** instance, we provide a decentralized platform where field imagery is treated as a public utility: fully downloadable, API-accessible, and privacy-compliant.

## The Infrastructure

Our field imagery pipeline is built on the **Panoramax** ecosystem, a federated open-source alternative to Google Street View that guarantees data permanence and open access. 

* **Storage**: High-performance object storage backend for hosting terabytes of 360° and flat field imagery.
* **Federation**: Our instance connects to the global Panoramax federation, ensuring that while the data is hosted in Canada, it is discoverable worldwide through the global panoramax catalog.

## The Processing Pipeline

We treat field imagery as a data engineering challenge, ensuring "time-to-insight" is minimized for downstream users.

1. **Ingestion**: Raw imagery is captured using diverse hardware (ex. 360° cameras, mobile rigs, meta glasses, etc.) and ingested by our systems. 
2. **Privacy & Anonymization**: Before publication, all imagery undergoes a rigorous privacy scrub. We utilize automated detection pipelines to blur faces and license plates, ensuring compliance with Canadian privacy standards while maintaining data utility.
3. **Standardization**: Images are processed into systems-ready formats, making it ready for analysis.
4. **Metadata Extraction**: We extract and normalize/strip identifiying information (ex. EXIF and GPS telemetry), indexing it into a **[FAIR Catalogue](https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/)**.

## Data Products

Unlike commercial platforms that only offer a "view" of the data, we provide the **data itself**.

* **API Access**: Full programmatic access via the Panoramax REST API for querying imagery by location, date, or sequence.
* **Bulk Datasets**: Curated dumps of street-level imagery available for computer vision training, asset management, and change detection models.
* **[FAIR Data Catalogue](https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/) Integration**: Seamless integration with geospatial workflows (ex. DuckDB, QGIS, Python, R, Julia, etc.).
