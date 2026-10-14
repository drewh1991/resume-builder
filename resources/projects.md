# Projects

Actual work completed. Use as a `Projects:` resume section or mix into job experience
when applicable.

## File Upload Pipeline

- Built a dynamic end-to-end file upload pipeline with UI, API, data ingestion, and normalized data modeling for bulk file submissions.
- Implemented a React/TypeScript frontend, secure signed URL uploads, and status tracking for customer file submissions.
- Used cloud object notifications to trigger Apache Airflow ingestion and Cloud Run parsing with metadata contract validation.
- Orchestrated reliable pipeline execution with Airflow and dbt-managed BigQuery models for downstream analytics.
- Enabled schema consistency and export-ready datasets for external service delivery.

## Apache Airflow/Google Cloud Composer Implementation

- Led the implementation of Apache Airflow/Google Cloud Composer to orchestrate data pipelines, moving away from a homegrown orchestration solution to ensure scalability and reliability as data processing needs grew.
- Designed and implemented dynamic, single-tenant, event-driven data pipelines using Apache Airflow, Python, and Google BigQuery to support scalable data processing for over 500 customers.
- Implemented dynamic pipeline generation in Airflow to automatically create and manage pipelines for new customers and data sources, enabling seamless onboarding and scalability.
- Implemented automated monitoring, alerting, and Slack integration for Airflow pipelines using Google Cloud's operations suite via Terraform, ensuring timely detection and resolution of pipeline issues.

## Automated Data Quality and Testing Framework

- Developed a scalable data quality and testing framework using dbt and Google Cloud Run to ensure the reliability and accuracy of data pipelines and models.
- Implemented an automated AI agent to triage and resolve dbt test failures, reducing manual intervention by 90% and improving data reliability.
- Designed and implemented a comprehensive set of dbt tests to validate data quality, including schema tests, data integrity tests, and custom business logic tests.
- Utilized Google Cloud Run to execute dbt tests on a scheduled basis and upon pipeline events, ensuring continuous validation of pipelines and models.

## Enterprise Retail Data Pipeline

- Designed and productionalized a high-volume retail data ingestion pipeline in BigQuery.
- Standardized transformation logic in dbt and normalized data models to improve query performance and downstream accessibility.

## Custom dbt Incremental Materialization

- Developed a custom dbt incremental materialization that reduced BigQuery compute costs by 80% for high-volume models.
- Optimized refresh patterns and history handling to maintain data accuracy while lowering operational expense.

## Connector Scaffolding Automation

- Built a proof-of-concept automation script that scaffolds new dbt connectors by generating direct, source, and cleaned layer models, mock data, and placeholder staging and normalized transformation files.
- Expanded the automation during a hackday with metadata-driven extensibility so new connectors can be modeled and onboarded faster.

## Data Modeling and dbt Standards

- Led Data Modeling guild efforts, documented model standards, and defined spike and dbt testing practices to improve model quality and reduce test noise.
- Modeled a major enterprise connector, re-modeled others, and mentored teammates through connector model delivery.

## Cloud Composer Proof of Concept

- Built a Cloud Composer proof-of-concept for high-volume ingestion and established Airflow as the foundation for future connector development.
- Developed a first custom Airflow Operator for connector authentication and documented the team's learning path for Airflow best practices.

## Enterprise Direct Connector

- Served as the technical lead for an enterprise direct connector, translating API requirements into prioritized implementation tasks and delivering ahead of schedule.
- Designed auth caching, report cadence scheduling, branch logic for backfills, export-skipping controls, and BigQuery load strategies using built-in operators.

## Marketplace API Implementation

- Led the implementation of a marketplace API integration and delivered 3 new connectors to unlock next-generation integrations.
- Built the streaming JSON parser capable of processing large datasets efficiently without memory or I/O issues.
- Sunset a legacy connector to reduce maintenance overhead and lower long-term operational risk.

## Vendor Portal Connector Improvements

- Reverse engineered a vendor portal API to reduce exported row counts by 95% and remove cell limit risk for large clients.
- Planned and executed a safe data model cutover to avoid production disruption while enabling backfill of two years of historical data.
- Improved connector stability, reduced errors and timeouts, and enabled enterprise-scale data ingestion.

## Space Planning Connector

- Led the development of a space planning connector from GCS-notified ingestion through a custom Airflow DAG and normalized data model to deliver a million+ dollar proof of value.
- Turned product PRD milestones into supportable technical work and partnered with teammates to accelerate delivery and confidence.
- Onboarded a teammate to the platform codebase while driving execution under a tight deadline.

## gRPC Implementation

- Standardized gRPC stub generation and publication to Artifact Registry to improve developer experience and remove manual stub management.
- Enabled seamless local development and service connectivity across multiple repositories.
- Unblocked connector development by providing a reliable, automated gRPC architecture for the platform.

## Portal Connector Automation

- Implemented Selenium-driven portal scraping for several distributor connectors, reducing custom connector work by identifying portal commonalities.
- Built a shared report configuration codebase for portal connectors and documented data point crosswalks to harmonized models.
- Created automated dbt cleaning steps to streamline ingestion and transform disparate portal data into clean, report-ready datasets.

## Data Platform Onboarding and Hiring

- Centralized and enhanced Data Platform onboarding documentation to help new hires ramp quickly.
- Participated in technical interviews for 6+ candidates and provided detailed feedback.
- Onboarded 3 new teammates through system overviews, shadowing sessions, learning tasks, and pull request review support.

## Data Platform Scaling

- Improved platform scalability by refining pipeline orchestration, monitoring, and cost controls for multi-tenant data workflows.
- Focused on reliability and maintainability while supporting growth from terabyte-scale batches to hundreds of terabytes of processed data.

## Snowflake Partner Ingestion Pipeline

- Productionalized a proof-of-concept partner pipeline into a production-grade Snowflake ingestion: 12 tables, ~50GB historical backfill and ~1GB daily, querying the Snowflake API and batching to Parquet on GCS.
- Built automated parity validation in dbt on top of the audit_helper plugin, evolving from partition-level to primary-key comparison, and fed summarized discrepancy reports back to the partner.

## Reverse ETL Destination Connector Platform

- Built and extended destination connectors end to end, from platform configuration through orchestration, data modeling, and export, across Snowflake, BigQuery, Redshift, Databricks, Azure, S3, Power BI, and Looker.
- Delivered curated warehouse data to 300+ customer destinations, including Snowflake exporter development for column-alias compatibility and export troubleshooting.
