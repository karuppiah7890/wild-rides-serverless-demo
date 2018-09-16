# Trying out serverless following

https://dev-ops-notes.com/aws/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s3-dynamodb-and-cognito

https://dev-ops-notes.com/cloud/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s3-dynamodb-and-cognito-part-2/

# Static Website Hosting

The static website was uploaded this way:

```
$ git clone https://github.com/awslabs/aws-serverless-workshops/
$ aws s3 sync ./aws-serverless-workshops/WebApplication/1_StaticWebHosting/website s3://wildrydes-karuppiah-natarajan
```
