# Setup Serverless

### Serverless is a platform for quickly creating and deploying our lambdas.

Serverless allows us to deploy our code to many different platforms, however we will be using Amazon Web Services due to its cost, ubiquity, and ease of use.  It will allow us to get quickly and easily deployed to the cloud.  If you're new to Serverless you can [read more about its capabilities here](https://serverless.com/).

![serverless-logo](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/serverless-logo.png)

---

To get started, install serverless on your machine: 

`npm install serverless -g`

And then login to your serverless account:

`serverless login`

Now we are set to create our serverless project.  From inside your repository directory execute the command:

`serverless create --template aws-nodejs`

---

### Awesome, now we're set up with a lambda that we can deploy to AWS.  Let's do it!

If you haven't set up AWS locally with your CLI you'll need to do so. 

1. First [register for an AWS account](https://portal.aws.amazon.com/billing/signup#/start). This requires a credit card but includes 12 months of free servies.  We aren't responsible for charges to your AWS account but the cost for this project should be free or just a few cents.

2. Next, [setup the aws-cli locally](https://docs.aws.amazon.com/polly/latest/dg/setup-aws-cli.html).

3. Re-work the serverless.yml file to look like this:

```
service: aws-nodejs

provider:
  name: aws
  runtime: nodejs8.10
  region: us-west-2

iamRoleStatements:
  - Effect: 'Allow'
    Action:
      - 'lambda:InvokeFunction'
    Resource: "*"

functions:
  hello:
    handler: handler.hello
    events:
      - http: ANY /
      - http: 'ANY {proxy+}'
```

In the `Provider` block we are specifying our Node version 8.10 that we would like to use, along with the region we would like to deploy the lambda into.  You can choose a region that is close to where you live.

Next we have added our `iamRoleStatements` to allow permissions for this lambda to be invoked.  For a production application we may want to limit this more extensively but for demo purposes this statement should work great.

Finally we will give the `events` key to our `functions` and use it to route all (ANY) of our requests through API gateway, for now. 

4. Deploy the lambda `serverless deploy`

Serverless should return some `endpoints` urls for you.  Pull the URL up in a browser to see your Lambda in action! https://qncdy5y2pg.execute-api.us-west-2.amazonaws.com/dev

You should see a message "Go Serverless v1.0! Your function executed successfully!" 🎉
