+++
title = "Backend Deployment"
chapter = true
weight = 2
pre = "<b>2. </b>"
+++

In this section, we will be using the AWS Amplify CLI and the Amplify Video Plug-in's VOD solution to deploy the AWS back end of our application. We will be relying on Amazon Elemental Mediaconvert for its file based transcoding capabilities, as well as originating our content from S3. **Note:** Since this is a workshop and we are not deploying a production environment, we will not be using a CloudFront Content Distribution Network(CDN) in front of the bucket. If you plan on using Amplify Video to launch production environments, remember to use CloudFront to reduce end to end latency.

 ![architecture](https://www.amplify-video.com/unicornflix/amplify_arch.png)
