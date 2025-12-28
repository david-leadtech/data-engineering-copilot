# Using Data Engineering Copilot for PLTV Pipeline Migration

The Data Engineering Copilot can significantly help with migrating and maintaining the PLTV pipeline in Dataform. Here's how:

## 🎯 How the Copilot Can Help

### 1. **Pipeline Development & Modification**

The copilot can:
- **Create new SQLX files** for PLTV stages
- **Modify existing stages** based on requirements
- **Add new transformations** or optimize existing ones
- **Fix compilation errors** automatically
- **Add assertions** for data quality checks

**Example:**
```
User: "Add a new stage to the PLTV pipeline that calculates customer retention rates"

Copilot:
1. Reads existing PLTV pipeline structure
2. Understands dependencies
3. Creates new SQLX file with proper config
4. Adds assertions
5. Updates dependencies in downstream stages
```

### 2. **Pipeline Compilation & Validation**

- **Compile the entire pipeline** to check for errors
- **Validate SQL syntax** before execution
- **Check dependencies** are correct
- **View the DAG** to understand data flow

**Example:**
```
User: "Compile the PLTV pipeline and show me any errors"

Copilot:
1. compile_dataform()
2. Analyzes errors
3. Suggests fixes
4. Can auto-fix common issues
```

### 3. **Execution & Monitoring**

- **Execute by tags**: Run only PLTV stages (`tags: ['pltv']`)
- **Execute by layer**: Run staging (`tags: ['staging', 'pltv']`), intermediate, or gold
- **Monitor workflow health**: Track success rates, duration, failures
- **Check pipeline health**: Get recommendations for optimization

**Example:**
```
User: "Run the PLTV staging tables and check if they succeed"

Copilot:
1. execute_dataform_by_tags(tags=['staging', 'pltv'])
2. get_workflow_status(workflow_invocation_id='...')
3. analyze_assertion_results(workflow_invocation_id='...')
4. Reports success/failures with details
```

### 4. **Error Analysis & Debugging**

- **AI-powered error analysis**: Understand BigQuery memory errors, timeouts, etc.
- **Find failed jobs**: Search by table, error type, or time period
- **Query optimization**: Get suggestions for performance improvements
- **Performance analysis**: Analyze query execution plans

**Example:**
```
User: "The PLTV pipeline failed with a memory error, help me fix it"

Copilot:
1. find_failed_bigquery_jobs(table_name='stg_pltv_dimensions_flattened', days=1)
2. analyze_bigquery_error(job_id='...')
3. Gets AI-powered analysis: "Memory error due to large JOIN. Suggestions: ..."
4. Can modify the SQLX file to implement fixes
```

### 5. **GitHub Integration (GitOps)**

- **Create branches** for PLTV changes
- **Sync Dataform → GitHub** automatically
- **Create pull requests** for review
- **Clean up merged branches**

**Example:**
```
User: "Create a branch for PLTV optimization changes and make a PR"

Copilot:
1. create_github_branch(branch_name='optimize-pltv-memory')
2. Modifies PLTV files
3. sync_dataform_to_github(...)
4. create_github_pull_request(...)
```

### 6. **Documentation Generation**

- **Generate pipeline documentation** automatically
- **Create dependency graphs**
- **Document transformations**

**Example:**
```
User: "Generate documentation for the PLTV pipeline"

Copilot:
1. generate_pipeline_documentation()
2. Creates comprehensive docs with:
   - All stages and their purposes
   - Dependencies graph
   - Data flow
   - Assertions
```

### 7. **Data Quality & Monitoring**

- **Check data quality anomalies**: Detect issues in PLTV tables
- **Analyze assertion results**: Review data quality checks
- **Monitor data freshness**: Ensure tables are updated on time

**Example:**
```
User: "Check if the PLTV pipeline data is fresh and has quality issues"

Copilot:
1. check_data_freshness(dataset_id='rosseca_apps_data', table_id='ltv_dimensions_e2e_calculation_looker')
2. check_data_quality_anomalies(table_name='ltv_dimensions_e2e_calculation_looker', days=30)
3. Reports: "Table last updated: 2 hours ago ✅", "Quality issues: None ✅"
```

## 🚀 Practical Workflows

### Workflow 1: Debugging a Failed PLTV Run

```
1. User: "The PLTV pipeline failed yesterday"
2. Copilot:
   - find_failed_bigquery_jobs(table_name='%pltv%', days=1)
   - analyze_bigquery_error(job_id='...')
   - Gets: "Memory error in stg_pltv_dimensions_flattened"
   - Reads the SQLX file
   - Suggests: "Add LIMIT for testing, optimize JOIN, add partitioning"
   - Can modify the file automatically
```

### Workflow 2: Adding a New PLTV Stage

```
1. User: "Add a new stage to calculate customer churn for PLTV"
2. Copilot:
   - Reads existing PLTV structure
   - Understands dependencies
   - Creates: int_pltv_churn_calculation.sqlx
   - Adds proper config, tags, assertions
   - Updates downstream dependencies
   - Compiles to validate
   - Creates PR for review
```

### Workflow 3: Optimizing PLTV Performance

```
1. User: "The PLTV pipeline is slow, optimize it"
2. Copilot:
   - analyze_query_performance(job_id='...') for each stage
   - get_query_execution_plan(query='...')
   - Identifies bottlenecks
   - suggest_query_optimization(query='...')
   - Modifies SQLX files with optimizations
   - Tests with dry-run
   - Creates PR
```

### Workflow 4: Monitoring PLTV Health

```
1. User: "Check the health of the PLTV pipeline"
2. Copilot:
   - check_pipeline_health(tags=['pltv'], days=7)
   - monitor_workflow_health(days=7)
   - get_failed_workflows(days=7)
   - Reports:
     * Success rate: 95%
     * Average duration: 12 minutes
     * 2 failures in last 7 days
     * Recommendations: "Consider adding retry logic"
```

## 📋 Current PLTV Pipeline Structure

Based on your existing pipeline:

```
definitions/
├── sources/
│   └── pltv_sources.sqlx          # Source declarations
├── silver/pltv/
│   ├── stg_pltv_dimensions_flattened.sqlx      # Stage 1
│   ├── stg_pltv_initial_purchases.sqlx         # Stage 2
│   ├── int_pltv_components.sqlx                # Stage 3
│   ├── int_pltv_product_aggregation.sqlx      # Stage 4-5
│   └── int_pltv_final_output.sqlx             # Stage 6-7
└── gold/pltv/
    └── ltv_dimensions_e2e_calculation_looker.sqlx  # Stage 8-9 (INCREMENTAL)
```

**Tags used:**
- `pltv` - All PLTV stages
- `staging,pltv` - Only staging tables
- `intermediate,pltv` - Only intermediate tables
- `gold,pltv` - Only gold layer
- `looker` - For Looker integration

## 🎯 Specific Use Cases for PLTV

### 1. **Fix Memory Errors**
The copilot can analyze BigQuery memory errors and suggest/implement fixes:
- Optimize JOINs
- Add partitioning
- Break down complex queries
- Add intermediate materializations

### 2. **Add New Metrics**
Want to add a new PLTV metric? The copilot can:
- Understand the current pipeline structure
- Add new calculations to appropriate stage
- Update downstream dependencies
- Add assertions for validation

### 3. **Optimize Incremental Processing**
The copilot can help optimize the incremental logic:
- Adjust `updatePartitionFilter` dates
- Optimize MERGE statements
- Add proper partitioning

### 4. **Add Data Quality Checks**
The copilot can add assertions:
- Non-null checks
- Unique key validations
- Custom business logic checks

### 5. **Documentation**
The copilot can generate comprehensive documentation:
- Pipeline architecture
- Data flow diagrams
- Transformation logic
- Dependencies

## 💡 Getting Started

### Setup the Copilot for PLTV Work

1. **Configure environment:**
   ```bash
   # In .env file
   DATAFORM_REPOSITORY_NAME=leadtech-dataform
   DATAFORM_WORKSPACE_NAME=your-workspace
   GITHUB_REPO_PATH=leadtechcorp/dataform-pltv-pipeline
   ```

2. **Use in Cursor:**
   ```python
   from data_engineering_copilot.agent import root_agent
   
   # Example: Check PLTV pipeline health
   result = root_agent.run("Check the health of the PLTV pipeline")
   ```

3. **Or use ADK web interface:**
   ```bash
   adk web
   # Then chat: "Check PLTV pipeline health"
   ```

## 🔗 Related Resources

- [Main README](README.md) - Full copilot capabilities
- [Cursor Integration](CURSOR_INTEGRATION.md) - Using in Cursor
- [PLTV Pipeline Docs](../leadtech-dataform/docs/PLTV_MIGRATION_SUMMARY.md) - Current PLTV documentation

