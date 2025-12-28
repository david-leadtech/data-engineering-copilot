# Changelog

All notable changes to the Dataform GitHub Agent will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-01-28

### Added
- Initial release of Dataform GitHub Agent
- **Dataform Integration (15 tools)**
  - Read/write SQLX files
  - Compile and validate pipelines
  - Execute workflows by name or tags
  - Monitor workflow health
  - Generate pipeline documentation
  - Analyze assertion results
  - Check data quality anomalies

- **dbt Integration (14 tools)**
  - Full dbt project management (run, test, compile, docs, seed, snapshot)
  - Execute models with selectors and tags
  - Generate documentation
  - Check source freshness
  - Execute custom macros

- **PySpark/Dataproc Integration (9 tools)**
  - Create and manage Dataproc clusters
  - Submit PySpark jobs
  - Create serverless batches
  - Monitor job execution

- **BigQuery Tools (9 tools)**
  - Query performance analysis
  - Execution plan analysis
  - Cost estimation
  - Data freshness tracking
  - **AI-powered error analysis and debugging**
  - Find failed jobs
  - Query optimization suggestions

- **GitHub Integration (11 tools)**
  - Read/write files
  - Create branches and PRs
  - Sync Dataform with GitHub
  - Create repositories
  - Clean up merged branches

- **GCS Tools (4 tools)**
  - List and read files from GCS buckets

### Total: 62 tools across all platforms

[1.0.0]: https://github.com/david-leadtech/dataform-github-agent/releases/tag/v1.0.0

