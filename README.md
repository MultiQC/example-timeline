# Apache Iceberg + Trino Performance Evaluation

This project sets up a development environment for evaluating Apache Iceberg with Trino compared to traditional Parquet for storing and querying MultiQC data directly from your S3 bucket.

## System Architecture

The setup includes:

- Direct connection to your AWS S3 bucket (s3://megaqc-test/)
- Trino as the SQL query engine
- Apache Iceberg for table format
- Hive Metastore for schema registry
- PostgreSQL for the metastore backend
- Jupyter Notebook for running queries and evaluations

## Getting Started

### Prerequisites

- Docker and Docker Compose
- Git
- AWS credentials with access to the s3://megaqc-test/ bucket

### Installation

1. Clone this repository:
   ```
   git clone <repository-url>
   cd example-timeline
   ```

4. Start the Docker containers:
   ```
   docker compose up -d
   ```

5. Wait for all services to start. You can check the status with:
   ```
   docker compose ps
   ```

### Accessing Services

- Jupyter Notebook: http://localhost:8888
- Trino UI: http://localhost:8080

## Running the Evaluation

1. Open Jupyter Notebook at http://localhost:8888
2. Navigate to `notebooks/iceberg_evaluation.ipynb`
3. Run all cells to execute the performance comparison

## Performance Evaluation

The notebook compares:

1. **Storage Time**: How long it takes to write data to Parquet vs. Iceberg
2. **Query Performance**: 
   - Filtering by metric name across all runs
   - Filtering by run_id and module_id

## Project Structure

- `docker-compose.yml` - Container configuration
- `trino/etc/` - Trino configuration files
- `notebooks/` - Jupyter notebooks for evaluation
- `exploring/` - Original Parquet test notebooks
- `.env` - Environment variables for AWS credentials

## Customization

- Adjust the dataset size in the notebook by changing `NUM_RUNS`, `NUM_MODULES`, etc.
- Modify query patterns to test different access patterns

## Potential Benefits of Iceberg

- Schema evolution capabilities
- Time travel (querying data as of a specific point in time)
- Better handling of small file problems
- Transactional consistency
- Partition evolution

## Troubleshooting

- If Trino fails to start, check the logs with `docker-compose logs trino-coordinator`
- If connections to AWS S3 fail, verify your credentials in the `.env` file
- If the Hive Metastore isn't accessible, check PostgreSQL is running correctly

## Additional Resources

- [Apache Iceberg Documentation](https://iceberg.apache.org/)
- [Trino Documentation](https://trino.io/docs/current/)
- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/) 