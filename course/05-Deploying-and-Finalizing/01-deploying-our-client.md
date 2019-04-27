# Deploying React client to AWS S3

### We have a our Lambda API deployed, let's get our React client deployed too

To get our React client deployed let's start off by building and compiling our code. In your React project's root directory run:

`npm run build`

This will create a bundle of files which we will be able to upload to AWS S3 hosting to serve to the world.

---

### Login to AWS Console

While the bundle is building login to the AWS console and navigate to AWS S3.

We will need to create a new S3 bucket for our project. I'm going to make one called `hello-serverless-world-client`.  Feel free to create it in whichever region is in your neck 
of the woods. 

![create-bucket](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/create-bucket.png)

Click into the bucket you just created and select `edit` in the box that contains `Manage public bucket policies`. Deselect `Block new public bucket policies` and `Block public and cross-account access if bucket has public policies` and then click `Save`. Now we can update our bucket policy with a public permission.

 Next, click into the `Bucket Policy` tab. We need to set public read access on this bucket in order to use it as a public facing website.  Here's the policy we will want to use, taken right from [docs.aws.amazon.com](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteAccessPermissionsReqd.html). 

```
{
  "Version":"2012-10-17",
  "Statement":[{
	"Sid":"PublicReadGetObject",
        "Effect":"Allow",
	  "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::example-bucket/*"
      ]
    }
  ]
}
```

Make sure to change `example-bucket` to your S3 bucket name you used. When you save that policy your public permissions should be all set.

---

### Upload our site file's

Click back to the Overview tab then select `upload`.  Simply drag and drop the contents of the `build` directory of your React client into the file uploader.  The build directory is the result of running `npm run build` a few steps back, and it contains our site packaged up for hosting.

Finally, click back into the Properties tab and select the `Static website hosting`.  You should see your `Endpoint` where anyone around the globe can access your website. For me, my website demo is at this url: (http://hello-serverless-world-client.s3-website-us-west-2.amazonaws.com)[http://hello-serverless-world-client.s3-website-us-west-2.amazonaws.com]

---

### Party! 🎉

Your web application built with React.js and AWS Lambda is deployed.  Move onto the last part of this course for the application code and other summarized takeaways. 🎓