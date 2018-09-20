# Trying out serverless following

https://dev-ops-notes.com/aws/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s3-dynamodb-and-cognito

https://dev-ops-notes.com/cloud/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s3-dynamodb-and-cognito-part-2/

# Extra things done and learned! 😄

## `sls` / `serverless` supports tab completion! 🎉

Tried this in `zsh` shell and it worked! The tab completion is supported for subcommands and for flags too 😁

## Overriding the default config for RAM allocated to the lambda function

The default config was 1028 MB RAM! That's a lot! Overrode it using `memorySize` in [`serverless.yml`](serverless.yml#L14) using :

```
memorySize: 128
```

## Checking the lambda function's logs using `sls` !

Tailed the logs using :

```
$ sls logs --function RequestUnicorn -t

START RequestId: 3feacab4-b9ae-11e8-af31-c357f5031e89 Version: $LATEST
2018-09-16 18:14:28.530 (+05:30)	3feacab4-b9ae-11e8-af31-c357f5031e89	Received event ( yu1wOsg2M4qyDZRT5A9ZxA ):  { path: '/ride',
  httpMethod: 'POST',
  headers:
   { Accept: '*/*',
     Authorization: 'eyJraWQiOiJLTzRVMWZs',
     'content-type': 'application/json; charset=UTF-8' },
  queryStringParameters: null,
  pathParameters: null,
  requestContext: { authorizer: { claims: [Object] } },
  body: '{"PickupLocation":{"Latitude":47.6174755835663,"Longitude":-122.28837066650185}}' }
2018-09-16 18:14:28.530 (+05:30)	3feacab4-b9ae-11e8-af31-c357f5031e89	Finding unicorn for  47.6174755835663 ,  -122.28837066650185
END RequestId: 3feacab4-b9ae-11e8-af31-c357f5031e89
REPORT RequestId: 3feacab4-b9ae-11e8-af31-c357f5031e89	Duration: 407.19 ms	Billed Duration: 500 ms 	Memory Size: 128 MB	Max Memory Used: 32 MB
```

Without tailing, the command is :

```
$ sls logs --function RequestUnicorn
```

## Invoking the lambda function using `sls` ! 🎉

Invoked the lambda function using :

```
$ sls invoke --path demos-and-examples/testEvent.json --function RequestUnicorn
```

It's an alternative to the tutorial's console based method to test the lambda function. This came in handy as it can be done from the command line itself which is what the tutorial is mostly trying to do - automating things using `serverless` and by doing almost everything from the CLI without using the console,like, even to get the ID of a resource for eg Cognito User Pool ID, we use `Outputs` in `serverless.yml` to see the output while deploying or after deploying using `sls info --verbose`. And for event data, it can be passed using a json file 😉.

## Testing the API Gateway Authorizer using `aws` CLI

Tested it using this command :

```
aws apigateway test-invoke-authorizer --rest-api-id <rest-api-id> --authorizer-id <authorizer-id> --headers Authorization=<token>
```

You need to replace the `<>` placeholders with actual values. The IDs were obtained as outputs while deploying using `sls deploy --verbose`, as it was part of the set of outputs in [`serverless.yml`](serverless.yml#L133)

## Locking serverless framework cli version

Locked it in [`serverless.yml`](serverless.yml#L4) using :

```
frameworkVersion: '=1.31.0'
```

This way, people using this service will be asked to use a sepecific `serverless` cli version to avoid inconsistency among teams and the CI tool too.

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

## Demos and Examples folder

I created a demos and examples folder to put some files into it, like the test event input json file, screenshot of how one of the logs looks like, raw logs of the tailed logs when I invoked a lambda a lot of times. You cam even see the execution times and billed times in them 😁

# Static Website Hosting

The static website was uploaded this way:

```
$ git clone https://github.com/awslabs/aws-serverless-workshops/
$ aws s3 sync ./aws-serverless-workshops/WebApplication/1_StaticWebHosting/website s3://wildrydes-karuppiah-natarajan
```
