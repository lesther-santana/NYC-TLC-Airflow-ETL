# NYC-TLC-ETL

The NYC-TLC-AIRFLOW-ETL repository is a comprehensive solution built with Apache Airflow DAG Running in Docker to extract High-Volume For-Hire Services parquet files from the year 2022, provided by the New York City Taxi and Limousine Commission (TLC), stored in an AWS bucket. The pipeline performs data transformation operations to cleanse and enrich the data before loading it into a Google BigQuery table. The purpose of this ETL pipeline is to prepare the data for consumption by a Looker Studio report, enabling detailed analysis and visualization of the trips by Uber and Lyft.

The DAG is manually triggered or via the API. However, we can easily modify the workflow to run on a  defined schedule, like running after the AWS bucket gets the latest High Volume FHV trip parquet file.

## Features

* Extraction of High-Volume FHV parquet files from the year 2022.
* Data transformation and cleansing operations.
* Loading of the transformed data into a Google BigQuery table.
* Manual triggering of the DAG or API-based triggering.
* Configurable scheduling to run the pipeline after the AWS bucket receives the latest High Volume FHV trip parquet file.

## Prerequisites
* Docker installed on your local machine.
* Google BigQuery project and credentials.
* AWS S3 bucket credentials.
## Setup

1. Configure the AWS S3 bucket connection

    In order to access the High-Volume FHV parquet files stored in the AWS S3 bucket, you need to configure the AWS S3 bucket connection in Apache Airflow. Follow the steps below:

    * Open the Airflow web interface.
    * Go to Admin > Connections.
    * Click on Create to create a new connection.
    * Set the Conn Id field to s3_conn.
    * Set the Connection Type to Amazon Web Services.
    * Fill in the AWS Access Key ID.
    * Fill in the AWS Secret Access Key.

1. To load the transformed data into a Google BigQuery table, you must to place the GOOGLE_APPLICATION_CREDENTIALS .json file in the "dags/" folder.

1. Create BigQuery Table with [Bigquery.ipynb](Bigquery.ipynb).

1. Set the Airflow variable

    The ETL pipeline requires an Airflow variable called HV_FHV_TABLE_ID, which is the ID of the BigQuery table where the transformed data will be loaded. Follow the steps below to set the variable:

    * Open the Airflow web interface.
    * Go to Admin > Variables.
    * Click on Create to create a new variable.
    * Set the Key field to HV_FHV_TABLE_ID.
    * Fill in the Value field with the ID of your BigQuery table.
    * Save the variable.

## Run
1. Configure files for the docker-compose. [For more information.](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html#running-airflow-in-docker)

    ``` bash
    mkdir -p ./logs ./plugins ./config
    echo -e "AIRFLOW_UID=$(id -u)" > .env
    ```

2. Create custom apache airflow image with gcloud API

    ``` bash
    docker build -t exented:latest .
    ```

3. Running Airflow

    ``` bash
    docker compose up
    ```