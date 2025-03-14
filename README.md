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

## Project Structure

The project follows a modular structure for better maintainability and reusability.

