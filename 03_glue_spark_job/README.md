# AWS Glue Spark Job

Before running this Glue Spark job, crawleres are created to create data catalog tables on raw CSV data present in ```s3://youtube-raw-us-west-1-<aws-account-id>-dev/youtube/raw_statistics/``` location. 

Appropriate column mappings are defined and null fields are dropped before final write in parquet format. Make sure to assign appropriate IAM roles to Glue Spark job with permissions to access required S3 locations.
