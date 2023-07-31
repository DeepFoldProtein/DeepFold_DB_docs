# gcputils.bigquery.BigQueryManager

## Overview

The `BigQueryManager` class provides an interface to interact with Google's BigQuery service. It requires the Google Cloud project ID during initialization and accepts a dry_run flag that if set to True, will only estimate the cost of query execution without actually executing them.

You can use this class to execute SQL queries, write the results to a table in a dataset, extract a table to a Google Cloud Storage bucket, and estimate the cost of running a SQL query.

## Attributes

- `project_id (str)`: The Google Cloud project ID.
- `dry_run (bool)`: If True, only the cost of queries will be estimated without actual execution.

## Methods

#### `__init__`

Initializes a new instance of the BigQueryManager class.

**Parameters:**

- `project_id (str)`: The Google Cloud project ID.
- `dry_run (bool, optional)`: If True, it only estimates the cost of queries without actually executing them. Defaults to False.

#### `howmuch`

Estimates the cost and the amount of data that a query will process.

**Parameters:**

- `query (str)`: The SQL query to be estimated.
- `job_config (Optional[bigquery.QueryJobConfig], optional)`: Job configuration for the BigQuery query job. Defaults to None.

**Returns:**

- None

#### `execute_query`

Executes a SQL query and returns the results as a pandas DataFrame.

**Parameters:**

- `query (str)`: The SQL query to be executed.

**Returns:**

- `Optional[DataFrame]`: The result of the query as a pandas DataFrame or None if dry_run is True.

#### `tobucket(self, storage_dir: str, file_name: str, dataset_id: str, table_name: str, compression: bool)`

Extracts a BigQuery table to a Google Cloud Storage bucket.

**Parameters:**

- `storage_dir (str)`: The Google Cloud Storage bucket where the table data will be extracted.
- `file_name (str)`: The name of the file to store the extracted data in Google Cloud Storage.
- `dataset_id (str)`: The ID of the dataset containing the source table.
- `table_name (str)`: The name of the BigQuery table from which data will be extracted.
- `compression (bool)`: If True, the extracted data will be compressed using GZIP; otherwise, no compression will be applied.

**Returns:**

- None

#### `writetable`

Executes a BigQuery SQL query and writes the results to a destination table in a dataset.

**Parameters:**

- `query (str)`: The SQL query to be executed.
- `destination_dataset (str)`: The name of the destination dataset where the table will be created to store the query results.
- `destination_table_name (str)`: The name of the destination table to store the query results.

**Returns:**

- None

## Example

```python
# Create a BigQueryManager instance
manager = gcputils.bigquery.BigQueryManager(project_id="your_project_id", dry_run=True)

# Use howmuch
manager.howmuch(query="your_query", job_config=bigquery.QueryJobConfig())

# Use execute_query
result_df = manager.execute_query(query="your_query")
print(result_df)

# Use tobucket
manager.tobucket(
    storage_dir="storage_dir",
    file_name="file_name",
    dataset_id="dataset_id",
    table_name="table_name",
    compression=True,
)

# Use writetable
manager.writetable(
    query="your_query",
    destination_dataset="destination_dataset",
    destination_table_name="destination_table_name",
)
```
