# Demo App 2

## Create Elastic Beanstalk Application

**Note!** the `--stack-name` parameter.

```
aws cloudformation create-stack --stack-name demo-app-2 --parameters ParameterKey=MyHostedZoneName,ParameterValue=example.com. --template-body file://../beanstalk.yml --profile example-account-dev --region eu-west-1
```

If you want to run this without custom domain, then remove `--parameters` from the command like this:

```
aws cloudformation create-stack --stack-name demo-app-2 --template-body file://../beanstalk.yml --profile example-account-dev --region eu-west-1
```

## Initialize Elastic Beanstalk command line interface

**Note!** that the same name that was in above command's `--stack-name` parameter is here as command line parameter.

```
eb init demo-app-2 --profile example-account-dev --region eu-west-1
```

## Deploy application

```
eb deploy
```

Note that if you want to deploy uncommited changes you must add `--staged` command line parameter. From `eb deploy --help`:

```
--staged              deploy files staged in git rather than the HEAD commit
```

## Testing

```
$ curl -D - http://demo-app-2.example.com
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Date: Thu, 12 Jul 2018 15:01:16 GMT
Server: nginx/1.12.1
Content-Length: 22
Connection: keep-alive

Hello from demo-app-2!
```

Or if you created the app without `MyHostedZoneName` parameter then the address is

```
curl -D - http://demo-app-2.eu-west-1.elasticbeanstalk.com
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Date: Thu, 12 Jul 2018 15:02:38 GMT
Server: nginx/1.12.1
Content-Length: 22
Connection: keep-alive

Hello from demo-app-2!
```
