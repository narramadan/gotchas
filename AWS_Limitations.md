# AWS Limitations to keep an eye when interacting with SDK

## S3

### ListObjectsV2 - Up to 1000

Returns max of 1000 objects in a bucket with each request. 

If there are more objects to retrieve, continue making requests until all objects are retrieved by checking for IsTruncated, which will determine if there are more objects to retrieve.

Ref: https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListObjectsV2.html
