---
title: "Data Dissemination Strategy"
toc: true
weight: 3
---

Our dissemination strategy prioritizes interoperability, long-term preservation, and decentralized resilience.

Once data products reach a production-ready state, the workflow is as follows:

* **Cloud-Native First:** Priority is given to highly performant, system-to-system file formats (e.g., Parquet) to enable highly performant applications.
* **Persistent Identification & Cataloging:** Every dataset version will be assigned a DOI for citation and immutability.
  * The endpoint `https://data-01.dataforcanada.org/processed/` will strictly serve the **latest** version of a dataset.
  * Global metadata will be aggregated into a single, queryable [STAC GeoParquet](https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/) file. This catalog will track all versions and DOIs, providing direct download links to [Zenodo](https://zenodo.org/communities/dataforcanada/) which serves as the long-term data repository.
* **Decentralized Distribution:** We will pilot BitTorrent to maximize infrastructure resilience. By leveraging [HTTP Web Seeding (BEP 19)](https://www.bittorrent.org/beps/bep_0019.html), torrents will be seeded simultaneously by Zenodo, the Data for Canada infrastructure, and community peers, ensuring high availability without a single point of failure.

## High-Level Overview

```mermaid

flowchart TD
    Sources[Open Data Sources]
    Processes[Transformation Processes]
    Artifacts[Systems-Ready Data]
    Portal[Object Storage]
    Metadata[Metadata]
    Distribution[Decentralized Distribution]
    Zenodo[Zenodo]
    Torrent[BitTorrent]
    Users[Researchers & Developers]
    Systems[Systems]

    Sources a1@--> Processes
    a1@{animate: true, animation: slow}
    Processes a2@--> Artifacts
    a2@{animate: true, animation: slow}
    Artifacts a3@--> Portal
    a3@{animate: true, animation: slow}
    Portal a4@--> Metadata
    a4@{animate: true, animation: fast}
    Metadata a5@--> Distribution
    a5@{animate: true, animation: fast}

    Distribution a6@--> Zenodo
    a6@{animate: true, animation: slow}
    Distribution a7@--> Torrent
    a7@{animate: true, animation: slow}

    Zenodo a9@--> Users
    a9@{animate: true, animation: slow}
    Torrent a10@--> Users
    a10@{animate: true, animation: fast}
    Torrent a11@--> Systems
    a11@{animate: true, animation: fast}
    Zenodo a12@--> Systems
    a12@{animate: true, animation: slow}
    Zenodo a13@--> Torrent
    a13@{animate: true, animation: slow}

    click Portal "https://data-01.dataforcanada.org/processed/" _blank
    click Metadata "https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/" _blank
    click Zenodo "https://zenodo.org/communities/dataforcanada/" _blank
```
