# Lambda Function

Raw JSON file looks like below:
```
{
 "kind": "youtube#videoCategoryListResponse",
 "etag": "\"ld9biNPKjAjgjV7EZ4EKeEGrhao/1v2mrzYSYG6onNLt2qTj13hkQZk\"",
 "items": [
  {
   "kind": "youtube#videoCategory",
   "etag": "\"ld9biNPKjAjgjV7EZ4EKeEGrhao/Xy1mB4_yLrHy_BmKmPBggty2mZQ\"",
   "id": "1",
   "snippet": {
    "channelId": "UCBR8-60-B28hp2BmDPdntcQ",
    "title": "Film & Animation",
    "assignable": true
   }
  },
  {
   "kind": "youtube#videoCategory",
   "etag": "\"ld9biNPKjAjgjV7EZ4EKeEGrhao/UZ1oLIIz2dxIhO45ZTFR3a3NyTA\"",
   "id": "2",
   "snippet": {
    "channelId": "UCBR8-60-B28hp2BmDPdntcQ",
    "title": "Autos & Vehicles",
    "assignable": true
   }
  },
  {
   "kind": "youtube#videoCategory",
   "etag": "\"ld9biNPKjAjgjV7EZ4EKeEGrhao/nqRIq97-xe5XRZTxbknKFVe5Lmg\"",
   "id": "10",
   "snippet": {
    "channelId": "UCBR8-60-B28hp2BmDPdntcQ",
    "title": "Music",
    "assignable": true
   }
  }
 ]
}
```

We are only interested in getting ```items``` from this nested JSON file. We could create a crawler to create a table on raw JSON data. But crawlers in AWS do not support the creation of tables on JSON data which are pretty formatted. So, JSON files are converted to parquet files to populate tables in AWS Glue Data Catalog.

Lambda function environment variables could look something like:
-	s3_cleansed_layer: s3://youtube-cleansed-us-west-1-[aws-account-id]-dev/youtube/cleansed_statistics_reference_data/
-	glue_catalog_db_name: db_youtube_cleansed
-	glue_catalog_table_name: cleansed_statistics_reference_data
-	write_data_operation: append

Lambda [trigger](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-edge-add-triggers-lam-console.html) is also created to run the lambda function every time a new JSON raw data file is placed in raw S3 bucket. Make sure to assign proper IAM role to the lambda function with access to required S3 locations.