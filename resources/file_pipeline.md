# Bulk File Ingestion Pipeline (Deep Dive)

Example deep-dive file. Use one of these per flagship project to capture the full
story in your own words; the short, resume-ready bullet version lives in
`projects.md`. Keep every fact here sourced to the candidate.

## Public phrasing notes

For anything that ends up on a resume or profile:

- Describe proprietary or internal formats generically instead of naming them.
- Say "seven-figure contract" instead of an exact contract value.
- Say "additional customers" instead of a count.
- Do not name customers.

## Project

- **Name:** End-to-End Bulk File Ingestion Pipeline
- **Role:** Pipeline Tech Lead (owned the project end to end)
- **Contribution share:** ~80% of the work
- **Timeline:** Greenfield. Proof of concept built from scratch in under 3 months, then productized into a sellable connector afterwards.

### Summary

Self-serve pipeline where customers upload proprietary data files and get
queryable, normalized data in about 10 minutes, cutting weeks-to-months of manual
prep down to minutes.

### Problem

- The source files describe product placement in a proprietary, hierarchical
  format with quirks from decades of evolution. Only a few tools can create them.
- Organizations pass these files around by hand and manage copies through complex
  manual processes; preparing for a quarterly retailer meeting could take weeks.
- There was no marketplace product turning raw placement data into insights.
- The pipeline reduced prep time to about 10 minutes for a single-file run.

### Architecture

- React front end: customer selects files; if a zip, the UI previews the contents
  and shows how nested directories will be flattened before commit.
- Upload writes to cloud object storage behind a signed URL, tagged with a
  trace_id that ties the whole run's pipeline events together.
- Object notifications are placed on a Pub/Sub topic; a subscription filters
  messages for the specific account (multi-tenant isolation).
- An Airflow sensor polls the subscription and triggers a Cloud Run job, which
  pulls messages, filters non-processable notifications, and defers acks until the
  end of the run so a failure never double-loads data.
- Work is split by trace_id; on ack, a pipeline lifecycle event updates the UI.
- On parse completion, data loads into a raw BigQuery table and the dbt DAG is
  triggered to transform; the exporter then delivers what the customer configured.
- Enrichment happens at parse time, not modeling time: metadata is passed to the
  parsing container via the CLI as a JSON object.
- Normalized data model: placements, fixtures, and stores; versioning is
  user-selected at upload.

### Personal contribution

- Pipeline tech lead; owned the project end to end (~80% of the work).
- The pipeline itself (ingestion and orchestration), the event-driven
  architecture, pipeline lifecycle events, the changelog and UI status model,
  error surfacing, and the normalized data model.
- Took the React front end from a teammate's starting point to production.

### Reliability

- A bad file fails in isolation; the rest of the run continues.
- Messages only ack on success, so a bad file is not reprocessed over and over.
- Errors surface in the UI with a badge and a click-through detail message, and
  are mirrored to an internal channel for immediate awareness.
- Alerts cover queue depth, time-on-queue, DAG failures, and dbt tests.

### Outcomes

- Greenfield proof of concept in under 3 months became a sellable connector sold
  to additional customers, plus add-on retailer connectors.
- Enabled a product-placement insight capability that did not exist in the
  marketplace.

### Scale

- 1 to 10,000 files in a single parse run; a single file is about 10 minutes end
  to end.

### Judgment

- Hardest problem: getting the event processing and acking semantics right.
- Next hardest: surfacing pipeline events in the UI.
- Next frontier: giving customers control of managing already-ingested files.

### Built by teammates

- The proprietary file-to-Parquet parser library.
- Some file-handling logic and domain expertise on metadata to collect.
- The initial React front end.
- The AI insights layer built on top of the data.
