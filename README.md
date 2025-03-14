# Sparkify Data Pipeline with Apache Airflow

## Overview

This project is aimed at creating an efficient, dynamic, and fully automated ETL pipeline for a music streaming company, **Sparkify**. The goal is to automate data processing, monitor the ETL workflow, and ensure the quality of the data being ingested into Sparkify's data warehouse on Amazon Redshift. Apache Airflow is used as the orchestration tool to facilitate these processes.

## Project Description

Sparkify has decided to introduce more automation and monitoring to their data warehouse ETL pipelines, and the best tool to achieve this is **Apache Airflow**. 

The project includes a high-grade data pipeline built with reusable tasks that are easy to monitor and can be backfilled when necessary. As data quality plays a crucial role in the analysis, the pipeline includes automated data quality checks to ensure that any discrepancies in the datasets are identified post-ETL execution.

The source data is stored in **Amazon S3** and needs to be processed into **Amazon Redshift**, Sparkify’s data warehouse. The source datasets consist of:

- **JSON Logs**: Containing information about user activity in the app.
- **JSON Metadata**: Containing information about the songs users listen to.

## Datasets

The datasets are hosted in S3 and can be found at the following locations:

- **Log data**: `s3://udacity-dend/log_data`
- **Song data**: `s3://udacity-dend/song_data`

### Key Files and Their Descriptions

- **`create_tables.sql`**: A one-time script used to create tables in Redshift for staging, dimension, and fact tables.
- **`sparkify_etl_dag.py`**: The main DAG definition, which includes the task definitions and links them together in the required order for execution.
- **`stage_redshift.py`**: Defines the `StageToRedshiftOperator` to copy data from S3 into staging tables in Redshift using the `COPY` command.
- **`load_dimension.py`**: Defines the `LoadDimensionOperator` to load data into dimension tables from the staging tables.
- **`load_fact.py`**: Defines the `LoadFactOperator` to load data into the fact tables from the staging tables.
- **`data_quality.py`**: Defines the `DataQualityOperator` to run data quality checks on the tables post-ETL.
- **`sql_queries.py`**: Contains all the SQL queries used for ETL tasks, including the `COPY` commands and data transformation queries.

## Requirements

- **Python 3**
- **Apache Airflow** (configured and installed)
- **Amazon Redshift** (with a running cluster)
- **Amazon S3** (for data storage)

### Setup and Configuration

1. **Create Redshift Cluster:**
   - First, create a Redshift cluster in your AWS environment and connect to it.
   - Run the provided `plugins/create_tables.sql` script to create the necessary tables in Redshift (staging, fact, and dimension tables).

2. **Set Up Airflow Connections:**
   - Make sure to configure two Airflow connections in the Airflow UI:
     - **AWS credentials connection**: Name it `aws_credentials`.
     - **Redshift connection**: Name it `redshift`.

3. **Airflow DAG Configuration:**
   - The Airflow DAG (`sparkify_etl_dag.py`) is set to run automatically according to your scheduling requirements. The DAG defines the task sequence for staging the data, loading dimension and fact tables, and performing data quality checks.

4. **Run the Pipeline:**
   - Trigger the Airflow DAG (`sparkify_etl_dag.py`) manually or based on the scheduled interval. The DAG will run the complete ETL process, transforming raw data from S3 into the Redshift warehouse, while performing data quality checks.

## How to Run

1. **Clone this repository:**

    ```bash
    git clone https://github.com/<your-username>/sparkify-etl-pipeline.git
    cd sparkify-etl-pipeline
    ```

2. **Install required dependencies:**

    Install dependencies in your virtual environment:

    ```bash
    pip install -r requirements.txt
    ```

3. **Set up Airflow:**

    If not already set up, install and configure Apache Airflow. You'll need to ensure that you have Airflow running and properly connected to both Redshift and AWS services via the connections described above.

4. **Run Airflow DAG:**

    Start your Airflow scheduler and web server:

    ```bash
    airflow scheduler
    airflow webserver
    ```

    Then, navigate to the Airflow UI and manually trigger the `sparkify_etl_dag` or let it run according to its scheduled interval.

## Monitoring and Backfilling

Apache Airflow provides an intuitive UI to monitor task execution. You can view logs, track the execution progress, and troubleshoot any failed tasks. The pipeline is designed to handle **backfilling** efficiently, meaning that you can easily rerun tasks for specific time intervals if necessary.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### Contact

For any questions or contributions, feel free to open an issue or submit a pull request.

---

### GitHub Repo

[https://github.com/<your-username>/sparkify-etl-pipeline](https://github.com/<your-username>/sparkify-etl-pipeline)

