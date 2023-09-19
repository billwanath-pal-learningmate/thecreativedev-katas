**Data Warehouse and Data Lake Architecture - Report Analytics**\
\
In architecture, We have a combination of a Data Lake and Data Warehouse to manage and analyze your data effectively. Below, I've detailed the components and processes involved in ELTV (Extract, Load, Transform, and Visualize) approach.\
\
**Data Ingestion (Extract):**
\
**DynamoDB to DynamoDB Stream to Lambda:**
- DynamoDB tables are the source of data.
- DynamoDB Streams capture changes in real-time.
- AWS Lambda functions process these changes and take appropriate actions.

#### Amazon Aurora to AWS DMS (Database Migration Service):
- Amazon Aurora databases are a source of structured data.
- AWS DMS is used to replicate data from Aurora to your Data Lake or Data Warehouse.

#### Client to Kinesis Firehose:
- Clients generate data that is sent to Kinesis Firehose in real-time.
- Kinesis Firehose collects and delivers this data to your data storage (S3 or Data Lake).

#### Google Analytics to Amazon AppFlow:
- Google Analytics data is extracted and transferred to Amazon AppFlow.
- Amazon AppFlow is responsible for securely moving and transforming the data.

### Data Loading (Load):

#### S3 Raw Data Passed to AWS Glue Crawler:
- Raw data is initially ingested into an S3 bucket.
- AWS Glue Crawler automatically discovers and catalogs this data.
- The cataloged metadata is stored in the AWS Glue Data Catalog.

### Data Transformation (Transform):

#### AWS Glue Data Catalog:
- Data from the Glue Data Catalog is used as the basis for transformation.
- AWS Glue Studio Jobs and AWS Lake Formation can access metadata for transformation tasks.

#### AWS Glue Studio Job:
- AWS Glue Studio is used for building and running ETL (Extract, Transform, Load) jobs.
- Data transformations are performed using Glue Studio to prepare data for analysis.

#### AWS Lake Formation:
- AWS Lake Formation may be used for fine-grained access control and data governance.
- It ensures that data access and transformation comply with security and compliance policies.

#### AWS S3 Refined Parquet Data:
- Transformed data is stored as Parquet files in S3.
- Parquet is an efficient columnar storage format ideal for analytics.

### Data Visualization (Visualize):

#### Amazon QuickSight Reports:
- Amazon QuickSight is used to create interactive and visually appealing reports.
- Reports are built on top of the transformed data, allowing users to gain insights.

#### Amazon Athena:
- Amazon Athena is used for querying data stored in S3.
- It provides an SQL-based interface for ad-hoc querying and analysis.

### Storage Components:

#### Amazon S3:
- S3 is used as both the raw data storage and storage for refined Parquet data.
- It serves as a cost-effective and scalable storage solution.

#### Iceberg:
- CDC (Change Data Capture) data is stored in Iceberg tables.
- Iceberg provides efficient and reliable storage for changing data.

### Query Engine:

#### Amazon Athena:
- Athena is the query engine used for ad-hoc querying of data.
- It supports SQL queries and can directly access data stored in S3.

This architecture allows to efficiently manage and analyze data from various sources, apply transformations, and visualize insights using services like Amazon QuickSight and Athena. The combination of Data Lake (S3) and Data Warehouse (Athena) offers scalability, flexibility, and cost-effectiveness for analytics needs.
