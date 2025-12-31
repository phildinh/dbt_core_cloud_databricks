### dbt Cloud (Github version control) + dbt Core (Local Collaboration VS code) + Databricks (Catalog, Schema, Data + connections)

---

## 📌 Executive Summary

This project demonstrates an **end-to-end analytics engineering workflow** built using **dbt and Databricks**, following a **Medallion Architecture (Landing → Bronze → Silver → Gold)**.  
The solution is designed to reflect **real-world, production-grade data engineering practices**, including governance, testing, version control, and automated deployments.

The project is intentionally split into **two complementary parts**:

- **Part 1 – dbt Cloud**: Managed execution, orchestration, and production deployment  
- **Part 2 – dbt Core + VS Code**: Local development and collaborative engineering workflows *(to be added)*

This structure showcases both **enterprise-ready cloud workflows** and **hands-on engineering capability**.

---

## 🏗️ Architecture Overview

The data platform follows a layered Medallion design:

<img width="332" height="222" alt="Screenshot 2025-12-31 114959" src="https://github.com/user-attachments/assets/44d95860-2486-4a6c-abcc-b7fb53746779" />

Key technologies:
- **Transformation:** dbt
- **Compute & Storage:** Databricks + Delta Lake
- **Governance:** Unity Catalog
- **Orchestration:** dbt Cloud Jobs
- **Version Control:** GitHub

---

## 🔹 Part 1 – dbt Cloud (Managed Analytics Engineering)

### Source Definition & Lineage

All raw datasets are declared using dbt **sources**, enabling:
- Explicit contracts between ingestion and transformation
- End-to-end lineage visibility
- Dependency-driven execution
- 
<img width="1909" height="908" alt="Screenshot 2025-12-31 113837" src="https://github.com/user-attachments/assets/1bab528b-4e68-4821-a093-600b90302a3e" />


This lineage demonstrates:
- Clear separation of concerns across layers
- Snapshot usage for slowly changing dimensions
- Tests attached directly to critical business models

---

### Bronze Layer – Raw Structured Data

The **Bronze layer** acts as the first structured representation of raw data.

Design principles:
- Materialized as **tables**
- Minimal transformation logic
- Schema alignment and type standardization only
- Optimized for traceability and replayability

Bronze models intentionally avoid business logic and serve as a stable foundation for downstream transformations.

---

### Snapshots – Slowly Changing Dimensions (SCD Type 2)

Snapshots are used to manage historical changes in dimensional data.

Key characteristics:
- Timestamp-based snapshot strategy
- Automatic tracking of valid-from and valid-to periods
- Preservation of historical states for accurate reporting

Snapshots integrate seamlessly with Silver models to enable time-aware analytics.

---

### Silver Layer – Business-Ready Models

The **Silver layer** transforms raw data into **cleaned, enriched, and business-aligned datasets**.

Responsibilities:
- Joining related entities
- Applying business rules and calculations
- Standardizing naming and metrics
- Preparing reusable datasets for analytics

Silver models are:
- Materialized as **tables**
- Fully tested
- Designed for reuse across multiple Gold use cases

---

### Gold Layer – Analytics & Reporting Models

The **Gold layer** exposes analytics-ready models for reporting and BI consumption.

Design principles:
- Business-level metrics only
- Aggregated at reporting grain
- Lightweight **view-based** materialization
- Optimized for query performance and flexibility

<img width="1909" height="904" alt="Screenshot 2025-12-31 114024" src="https://github.com/user-attachments/assets/9ea13545-21ac-4295-8379-ab1017b9a5ad" />

---

### Testing Strategy

Data quality is enforced using multiple testing layers:

- **Schema tests** (uniqueness, not-null constraints)
- **Unit tests** validating calculations and aggregations
- **Snapshot tests** ensuring historical consistency

All tests are executed automatically as part of `dbt build`, ensuring production reliability.

---

### Version Control & Change Management

The project is integrated with GitHub through dbt Cloud version control.

<img width="1897" height="905" alt="Screenshot 2025-12-31 113943" src="https://github.com/user-attachments/assets/faa410fb-6629-4cba-b3cb-53af8969133c" />

This enables:
- Branch-based development
- Safe change isolation
- Clear audit history of transformations

---

### Production Deployment & Orchestration

Transformations are deployed using **dbt Cloud jobs** targeting a production Databricks catalog.

<img width="1897" height="921" alt="Screenshot 2025-12-31 114335" src="https://github.com/user-attachments/assets/9b8db783-8a9a-4014-ba89-25e1686b6a4c" />

The production run demonstrates:
- Incremental model execution
- Snapshot processing
- Automated test enforcement
- Successful deployment with no runtime errors

---

## 🔹 Part 2 – dbt Core + VS Code (Collaborative Development)

🚧 *Planned Extension*

This section will demonstrate:
- Local dbt Core setup connected to Databricks
- VS Code–based development workflows
- Developer-specific schemas for isolated testing
- Collaboration patterns between multiple engineers
- Consistency between local and dbt Cloud execution

This mirrors real-world team-based analytics engineering environments.

Setup connections from VS Code (clone repo via Github and install UV package then setup connection)
<img width="1908" height="1031" alt="image" src="https://github.com/user-attachments/assets/017f0538-3c78-491b-983f-3f4b6350a44e" />

---

## 🚀 Skills Demonstrated

- Analytics engineering with dbt
- Databricks + Delta Lake architecture
- Medallion data modeling
- SCD Type 2 snapshot design
- Data quality testing (schema & unit tests)
- Lineage-driven development
- Git-based collaboration
- Production orchestration with dbt Cloud

---

## 🧠 Key Learnings

- Clear layer separation simplifies governance and maintenance
- Snapshots are critical for historical accuracy
- Tests significantly reduce production risk
- dbt Cloud accelerates production readiness
- Strong naming conventions improve lineage readability

---

## 📈 Future Enhancements

- Complete dbt Core + VS Code workflow
- Introduce environment-based configuration (dev vs prod)
- Add CI checks on pull requests
- Generate and publish dbt documentation
- Expand Gold models for downstream BI tools

---

## 📂 Repository Structure

```text
.
├── models/
│   ├── landing/
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── snapshots/
├── tests/
├── macros/
├── seeds/
├── dbt_project.yml
├── packages.yml
└── README.md
