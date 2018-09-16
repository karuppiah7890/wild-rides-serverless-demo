# Trying out serverless following

https://dev-ops-notes.com/aws/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s3-dynamodb-and-cognito

https://dev-ops-notes.com/cloud/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s3-dynamodb-and-cognito-part-2/

# Extra things done

## Locking serverless framework cli version

Locked it in [`serverless.yml`](serverless.yml#L4) using :

```
frameworkVersion: '=1.31.0'
```

## Using [Serverless Dashboard](https://serverless.com/dashboard/)

Signed up for [Serverless Dashboard](https://dashboard.serverless.com) and created an app `serverless-demo`. used the `app` and `tenant` config in [`serverless.yml`](serverless.yml#L2) like this :

```
app: serverless-demo
tenant: karuppiah7890
```

and then logged into serverless platform using :

```
sls login
```

and then deployed the service (in verbose mode) using :

```
sls deploy -v
```

Then checked the dashboard of the app at https://dashboard.serverless.com/tenants/karuppiah7890/applications/serverless-demo/ and it showed services list which contained `wild-rides-serverless-demo` and it's info was present at https://dashboard.serverless.com/tenants/karuppiah7890/applications/serverless-demo/services/wild-rides-serverless-demo/

> Note:
> An application (app) can contain many services. A service may contain many serverless functions.
> And Serverless Dashboard supports multiple applications.

# Static Website Hosting

The static website was uploaded this way:

```
$ git clone https://github.com/awslabs/aws-serverless-workshops/
$ aws s3 sync ./aws-serverless-workshops/WebApplication/1_StaticWebHosting/website s3://wildrydes-karuppiah-natarajan
```
