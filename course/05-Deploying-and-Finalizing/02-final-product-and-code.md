# Final Product

### Our finished demo

![finished-demo](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/finished-demo.png)

[http://hello-serverless-world-client.s3-website-us-west-2.amazonaws.com/](http://hello-serverless-world-client.s3-website-us-west-2.amazonaws.com/)

Our demo might be finished but there are many ways to extend this project.  We can start to add more routes and endpoints to our client and lambda and build a full features app.  Some great next steps could be styling our application and adding more [Github API](https://developer.github.com/v3/) features.

---

### Total Cost

This minimal website is 166KB and at the S3 Standard rate of `$0.023 / GB` We can expect to pay not more than a few pennies a month to serve these React and HTML files. 

Our Lambda is similarly inexpensive.  We can expect to pay just `$0.20 per 1 million` invocations of our Lambda.

We are also using API gateway, which is $3.50 per million requests. 

All together this setup is unlikely to cost more than $5.00 a month at low traffic volumes. And that's if you aren't still on free tier pricing, which should treat your pockets even nicer.  We aren't responsible for your AWS bill though, so [keep a close eye on it](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/monitoring-costs.html)!

---

### Repositories for the final product

#### [hello-world-serverless-lambda](https://github.com/compcuter/hello-world-serverless-lambda)
#### [hello-world-serverless-client](https://github.com/compcuter/hello-world-serverless-client)

`We welcome pull requests, comments, and suggestsions 😊` 

See the README.md of each repository for instructions on how to get up and running!

I hope you enjoyed the course, have fun making!
---






