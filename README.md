# Sparkify Data Lake

## Overview

This project implements an ETL data pipeline for the music streaming app Sparkify.


The data is extracted from a data lake of files in JSON format and stored in a star schema in parquet format.
Both input and output data are stored in AWS S3 and pyspark, Python library interacting with the Spark framework, pyspark, is used for distributed data processing.

The output data is optimized for OLAP because of the use of a star schema.
The schema is created via the `schema-on-read` approach during the ETL process
performed by a Python script.

## Structure

```bash
├── README.md - This file.
├── data - folder containing sample data
├── etl.py # Python script performing all DDL and ETL tasks.
└── dl.cfg # Config file to be populated with credentials for accessing all cloud resources.
``` 

## Analytics Schema

The analytics tables centers on the following fact table:

* `songplays` - which contains a log of user song plays

`songplays` has foreign keys to the following (self-explanatory) dimension tables:

* `users`
* `songs`
* `artists`
* `time`

## Instructions

* Create a S3 bucket to store the input and output
* Extract the songs data from data folder and copy it to `<AWS_S3_BUCKET>/data/song_data`
* Extract the logs data from data folder and copy it to `<AWS_S3_BUCKET>/data/log_data`
* Create the folder  `<AWS_S3_BUCKET>/output/`
* Create IAM credentials authorized to read from and write to the bucket you created
* Update `dl.cfg` with the following:
```
[AWS]
AWS_ACCESS_KEY_ID=<your_aws_access_key_id>
AWS_SECRET_ACCESS_KEY=<your_aws_secret_access_key>
AWS_S3_BUCKET=<your_s3_bucket_name>
```
* To execute the ETL pipeline from the command line, run `python etl.py` and the results will be stored at `<AWS_S3_BUCKET>/output`