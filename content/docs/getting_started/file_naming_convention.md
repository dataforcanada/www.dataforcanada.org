---
title: File Naming Convention
weight: 2
next: /docs/processes
sidebar:
  open: true
---

## Data for Canada: File Naming Convention (DFC-FNC)

### 1. The Current Schema

All published datasets must adhere to the following structure to ensure files are machine-parsable, sortable by region, and identifiable by human readers. **This file naming convention will be modified as we solidify our processes**.

{{< callout >}}
We are open to feedback on the current file naming convention.
{{< /callout >}}

#### **Syntax**

`[iso-region]_[source-identifier]_[theme]_[iso-date]_[variant].[extension]`

**Example**:
`ca-ab_edmonton-2023A00054811061_orthoimagery_2023_075mm.pmtiles`

#### **Component Breakdown**

| Segment | Definition | Format / Rules | Example |
| --- | --- | --- | --- |
| **1. ISO Region** | The ISO 3166-2 code for the jurisdiction. | Lowercase. Hyphenated. | `ca-ab`, `ca` |
| **_** | *Separator* | Underscore |  |
| **2. Source / Location ID** | **Organization** OR **Location**. | Use `[colloquial-name]-[dguid]` for locations, OR `[organization-name]` for national bodies. | `edmonton-2023A00054811061` OR `statcan` |
| **_** | *Separator* | Underscore |  |
| **3. Theme** | The primary category or title of the dataset. | Lowercase. **snake_case** allowed for longer titles. | `orthoimagery`, `open_database_of_buildings` |
| **_** | *Separator* | Underscore |  |
| **4. ISO Date** | The vintage of the data source. | **ISO 8601**. Flexible precision. | `2023`, `2023-06`, `2023-06-01` |
| **_** | *Separator* | Underscore |  |
| **5. Variant** | Resolution or specific subset info. | **No Projections.** Alphanumeric. Units included. | `075mm`, `30cm` |

## 2. Component Detail

### A. Source / Location ID (Flexible)

This segment defines the "Who" or "Where" of the dataset.

* **For Geographic Datasets:** Use the **Colloquial Name** + **Hyphen** + **DGUID**.
* *Example:* `edmonton-2023A00054811061`


* **For Organization Datasets:** Use the **Organization Acronym** when the data is national or not tied to a single DGUID.
* *Example:* `statcan`, `cmhc`, `nrcan`

### B. The DGUID (Capitalization Exception)

If using a DGUID (Dissemination Geography Unique Identifier), you must adhere to Statistics Canada standards.

* **Link:** [Statistics Canada: DGUID Definition](https://www12.statcan.gc.ca/census-recensement/2021/ref/dict/az/definition-eng.cfm?ID=geo055)
* **Rule:** While the rest of the filename is lowercase, you **must capitalize the structural type letter** (e.g., 'A' for Administrative areas, 'S' for Statistical areas) within the DGUID.
* **Example:** `2021A0005...` (Correct) vs `2021a0005...` (Incorrect).

### C. ISO Date Flexibility

Dates follow strictly **ISO 8601**, but the precision can vary based on the nature of the data (Year, Month, or Day).

* **Learn More:** [Wikipedia: ISO 8601 Date and Time Format](https://en.wikipedia.org/wiki/ISO_8601)

**Examples of Date Precision:**

* **Month Precision:** `ca_statcan_national_address_register_2024-12.parquet`
* **Day Precision:** `ca_statcan_open_database_of_buildings_2025-04-15.parquet`

### D. Variant

This field is strictly for **resolution** (e.g., `075mm`, `1m`) or content subsets.

* **Rule:** **Do not include projection information** (e.g., `EPSG:3857`, `NAD83`) in the filename.
* **Reasoning:** Projection details are handled exclusively in the file format metadata or the accompanying **[FAIR Data Catalog](https://stac-utils.github.io/stac-geoparquet/latest/spec/stac-geoparquet-spec/)** item.

## 3. Example Scenarios

### **Scenario 1: High-Res Orthoimagery (Location Based)**

* **Context:** 7.5cm pixel resolution imagery of Edmonton, Alberta from 2023.
* **File Name:** `ca-ab_edmonton-2023A00054811061_orthoimagery_2023_075mm.pmtiles`
* **Reference:** [Preview and Download Orthoimagery](https://www.dataforcanada.org/docs/processes/orthoimagery/#download-and-preview)

### **Scenario 2: National Organization Data (Source Based)**

* **Context:** The Open Database of Buildings released by Statistics Canada on April 15, 2025.
* **File Name:** `ca_statcan_open_database_of_buildings_2025-04-15.parquet`
* **Reference:** [Preview and Download Census Data](https://www.dataforcanada.org/docs/processes/statistical_products/statistics_canada/census_data/#how-to-use-the-map-preview)

## 4. Helper Tools

### **Statistics Canada Geography Search**

To accurately populate the **Location ID** segment of the schema, use this tool to find 2021 Census geographies and their corresponding DGUIDs.

* **Tool URL:** [https://statcan-geography.labs.dataforcanada.org/](https://statcan-geography.labs.dataforcanada.org/)
* **Source Code:** [GitHub Repository](https://github.com/dataforcanada/statcan-geography.labs.dataforcanada.org)
* **Usage:** Enter a city or region name to retrieve the correct colloquial name and DGUID pairing (e.g., searching "Ottawa" returns `2021A00053506008`).
