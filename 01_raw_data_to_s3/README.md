# Copy raw data to an AWS S3 bucket

- Create two S3 buckets:
  - youtube-raw-us-west-1-[aws-account-id]-dev/youtube/raw_statistics/
  - youtube-raw-us-west-1-[aws-account-id]-dev/youtube/raw_statistics_reference_data
- Setup AWS CLI using the IAM user access key and secret key
- Run the shell commands to push raw files to created S3 buckets