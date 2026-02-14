---
title: File Naming Convention
weight: 2
next: /docs/processes
sidebar:
  open: true
---

## Data for Canada: File Naming Convention (DFC-FNC)

## Background

{{< callout type="important" >}}
  You will need to understand these concepts to fully grasp the file naming convention.
{{< /callout >}}

See Statistics Canada's [geographic hiearchy](https://www12.statcan.gc.ca/census-recensement/2021/ref/dict/fig/index-eng.cfm?ID=F1_1) and use the [Census of Population 2021 Dictionary](https://www12.statcan.gc.ca/census-recensement/2021/ref/dict/az/index-eng.cfm) to understand their conceptual model of representing Canada.

![geographic hierarchy](geographic-hiearchy.svg).

### 1. The Current Schema

All published datasets must adhere to the following structure to ensure files are machine-parsable, sortable by region, and identifiable by human readers. **This file naming convention will be modified as we solidify our processes**.

{{< callout >}}
We are open to feedback on the current file naming convention.
{{< /callout >}}

#### **Syntax**

`[iso-region]_[source-identifier]-[DGUID]_[packages_collection]_[iso-date]_[variant]_[version].[extension]`

**Example**:
`ca-ab_city-of-edmonton-2023A00054811061_orthoimagery_2023_075mm_v0.0.1.pmtiles`

#### **Component Breakdown**

| Segment | Definition | Format / Rules | Example |
| :--- | :--- | :--- | :--- |
| **1. ISO Region** | The [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-2:CA), which is a two-letter country code, or [ISO 3166-2](https://www.iso.org/obp/ui/#iso:pub:PUB500001:en) which identifies the principal subdivisions (ex. provinces, states, etc.) | Lowercase. Hyphenated. | `ca`, `ca-ab` |
| **_** | *Separator* | Underscore |  |
| **2. Data Source and DGUID** | **Data Source and DGUID**. | Use `[data-source-name]` for the data source and the DGUID for the geographic area it covers. | `city-of-edmonton-2023A00054811061`, `statcan-2021A000011124` |
| **_** | *Separator* | Underscore |  |
| **3. Package** | The package name for the dataset (see [High-Level Overview](https://www.dataforcanada.org/#high-level-overview)). | Lowercase. **snake_case** allowed for longer titles. | `orthoimagery` |
| **_** | *Separator* | Underscore |  |
| **4. ISO Date** | The vintage of the data source. | **ISO 8601**. Flexible precision. | `2023`, `2023-06`, `2023-06-01`, `2026-02-11T19:50:58` |
| **_** | *Separator* | Underscore |  |
| **5. Variant** | Resolution or specific subset info. | **No Projections.** Alphanumeric. Units included. | `075mm`, `30cm` |
| **_** | *Separator* | Underscore |  |
| **6. Version** | **Semantic Versioning**. | `v[Major].[Minor].[Patch]` | `v0.0.1` |

## 2. Component Detail

### A. Source / Location ID (Flexible)

This segment defines the "Who" of the dataset.

* Use the **Data Source Name** + **Hyphen** + **DGUID**.
  * *Example:* `city-of-edmonton-2023A00054811061`

### B. The DGUID (Capitalization Exception)

If using a DGUID (Dissemination Geography Unique Identifier), you must adhere to Statistics Canada standards.

* **Link:** [Statistics Canada: DGUID Definition](https://www12.statcan.gc.ca/census-recensement/2021/ref/dict/az/definition-eng.cfm?ID=geo055)
* **Rule:** While the rest of the filename is lowercase, you **must capitalize the structural type letter** (e.g., 'A' for Administrative areas, 'S' for Statistical areas) within the DGUID.
* **Example:** `2021A0005...` (Correct) vs `2021a0005...` (Incorrect).

### C. ISO Date Flexibility

Dates follow strictly **ISO 8601**, but the precision can vary based on the nature of the data (Year, Month, or Day).

* **Learn More:** [Wikipedia: ISO 8601 Date and Time Format](https://en.wikipedia.org/wiki/ISO_8601)

**Examples of Date Precision:**

* **Month Precision:** `ca_statcan-2024A000011124_2024-12_v0.0.1.parquet`
* **Day Precision:** `ca_statcan-2025A000011124_2025-04-15_v0.0.1.parquet`

### D. Variant

This field is strictly for **resolution** (e.g., `075mm`, `1m`) or content subsets.

* **Rule:** **Do not include projection information** (e.g., `EPSG:3857`, `NAD83`) in the filename.
* **Reasoning:** Projection details are handled exclusively in the file format metadata or the accompanying **[FAIR Data Catalogue](https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/)** item.

### E. Semantic Versioning

We use **SemVer** (`vMAJOR.MINOR.PATCH`) to track changes to datasets.

* **Link:** [SemVer.org](https://semver.org/)

| Component | Logic for Data | Example Scenario |
| :--- | :--- | :--- |
| **MAJOR** | **Breaking Change.** The schema changed, columns were renamed/removed, or the meaning of the data changed significantly. Old code will break. | `v0.0.1` → `v1.0.0`<br>*(Renamed column `geo_id` to `dguid`)* |
| **MINOR** | **New Feature (Non-Breaking).** New columns were added, or coverage was expanded, but old columns remain. Old code still runs. | `v0.0.1` → `v0.1.0`<br>*(Added a `population_density` column)* |
| **PATCH** | **Bug Fix.** Incorrect data values were fixed, but the schema (columns) is identical. | `v0.0.1` → `v0.0.2`<br>*(Fixed typo in metadata or coordinate precision)* |

## 3. Helper Tools

### **Statistics Canada Geography Search**

{{< callout type="warning" >}}
  In the tool below, you can click on each individual **DGUID** to see their associated geography.
{{< /callout >}}

To accurately populate the **DGUID** segment of the schema, use this tool to find 2021 Census geographies and their corresponding DGUIDs.

* **Tool URL:** [https://statcan-geography.labs.dataforcanada.org/](https://statcan-geography.labs.dataforcanada.org/)
* **Source Code:** [GitHub Repository](https://github.com/dataforcanada/statcan-geography.labs.dataforcanada.org)
* **Usage:** Enter a city or region name to retrieve the correct colloquial name and DGUID pairing (e.g., searching "Ottawa" returns `2021A00053506008`).
