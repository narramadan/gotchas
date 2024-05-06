# AWS Limitations to keep an eye when interacting with SDK

## S3

### ListObjectsV2 - Up to 1000

Returns max of 1000 objects in a bucket with each request. 

__Solution:__

If there are more objects to retrieve, continue making requests until all objects are retrieved by checking for IsTruncated, which will determine if there are more objects to retrieve.

__Ref:__

* https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListObjectsV2.html

## API Gateway

### Default limit for Lambda invocation 

API Gateway requests will timeout after 29 sec for lambda invocations which cannot be changed. API gateway will throw 504 timeout error if not responded within 29 secs.

__Solution:__

* Use asynchronous execution pattern - https://joarleymoraes.com/serverless-long-running-http-requests/

__Ref:__

* https://docs.aws.amazon.com/apigateway/latest/developerguide/limits.html
