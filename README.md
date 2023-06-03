# NYC-TLC-ETL

The NYC-TLC--AIRFLOW-ETL repository is a comprehensive solution built with Apache Airflow DAG Running in Docker to extract High-Volume For-Hire Services parquet files from the year 2022, provided by the New York City Taxi and Limousine Commission (TLC), stored in an AWS bucket. The pipeline performs data transformation operations to cleanse and enrich the data before loading it into a Google BigQuery table. The purpose of this ETL pipeline is to prepare the data for consumption by a Looker Studio report, enabling detailed analysis and visualization of the trips by Uber and Lyft.

The DAG is manually triggered or via the API. However, we can easily modify the workflow to run on a  defined schedule, like running after the AWS bucket gets the latest High Volume FHV trip parquet file.
