+++
title = "Recap"
chapter = true
weight = 50
pre = "<b>4. </b>"
+++

Let's take a brief look at what was just created:

  ![architecture](https://www.amplify-video.com/unicornflix/amplify_arch.png)

The video processing plane of Amplify Video VOD uses an S3 bucket for source material that generates S3 events on object PUT. A Lambda Function, triggered from the S3 event, schedules the MediaConvert job to process  content. The outputs of MediaConvert are put into the Output S3 bucket and also generate S3 events on object PUT. These events trigger a final Lambda function which sets access policies on the content served to users in the output bucket.

The data plane consists of AppSync hosted GraphQL APIs, Lambda Resolvers, and DynamoDB as the persistance layer for video metadata and access URLs. 

Authentication for the web application is governed through Cognito User Pools, which protect access to the GraphQL API. The API has fine-grained access based on the group in the Cognito User Pool. Cognito also generates temporary, limited-privilege AWS credentials for access to upload content into S3.


With the infrastructure deployed, let's test processing and streaming a video asset. 

1. Open the S3 console and upload a small video file to the 'Input Storage Bucket' which was returned when you ran amplify push. You can download and upload [this sample clip](https://www.amplify-video.com/unicornflix/sample2.mp4) or [this other sample clip](https://www.amplify-video.com/unicornflix/sample.mp4) if you don't have your own video handy. **Tip:** Right click on the link and select `Save as...` to grab the clip.
1. Check the MediaConvert console, you should see an asset in 'progressing' shortly after the upload to S3 completes. Once the MediaConvert job is finished, continue on to the next step.
1. Click the checkbox in the S3 console next to the .m3u8 object to open the information panel. Copy the Object URL and paste it into safari, iOS, VLC, or by using a test player like the [Amplify Video Stream Tester](https://www.amplify-video.com/Player)

Congratulations, you are now hosting a Video-on-Demand platform on AWS! Now let's setup a website that we will use to upload more content and deliver it to viewers. 

