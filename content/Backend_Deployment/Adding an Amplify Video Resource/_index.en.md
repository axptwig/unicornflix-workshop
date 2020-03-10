+++
title = "Adding an Amplify Video Resource"
date = 2020-03-09T12:03:35-07:00
weight = 10
chapter = true
pre = "<b>2. </b>"
+++

1. Now, we are going to add the amplify video module to the project. 
    * `amplify video add`
1. Follow the prompts as shown below. We'll be building in a basic content management system (CMS) as part of our video-on-demand (VOD) platform.
<pre>
unicornflix <b>$amplify add video</b>
? Please select from one of the below mentioned services: <b>Video On Demand (beta)</b>
? Provide a friendly name for your resource to be used as a label for this category in the project: <b>unicornflix</b>
? Select a system-provided encoding template, specify an already-created template name:  <b>Default Encoding Template (Apple HLS
 @ 1080p30)</b>
? Is this a production enviroment? <b>No</b>
? Do you want Amplify to create a new GraphQL API to manage your videos? <b>Yes</b>
</pre>

Above we created the first part of amplify video to support transcoding of files. This workflow stands up two S3 buckets with a pre-processing Lambda function - to create new MediaConvert jobs for the files uploaded - and a post-processing Lambda function - to register the completed job and make the content available for playback. The MediaConvert job is configured to use the template you choose in the prompts above. If we had chosed <b>Yes</b> for the production environment question, Amplify video would spin up AWS CloudFront to host your content on a CDN.

<pre>
Video On Demand only supports GraphQL right now.
If you want to only use API for CMS then choose the default ToDo and don't edit it until later.
? Please select from one of the below mentioned services: <b>GraphQL</b>
? Provide API name: <b>unicornflix</b>
? Choose the default authorization type for the API <b>Amazon Cognito User Pool</b>
</pre>

Above we dive into create the basic infrastructure for our API. Amplify Video for Video on Demand only supports using GraphQL powered by AWS AppSync.

<pre>
? Do you want to use the default authentication and security configuration? <b>Default configuration</b>
? How do you want users to be able to sign in? <b>Username</b>
? Do you want to configure advanced settings? <b>No, I am done.</b>
Successfully added auth resource
</pre>

We take advantage of the built in Auth component for Amplify to add basic authentication to our application. We will keep with the defaults as it supports what we need for our application.

<pre>
? Do you want to configure advanced settings for the GraphQL API <b>No, I am done.</b>
? Do you have an annotated GraphQL schema? <b>No</b>
? Do you want a guided schema creation? <b>Yes</b>
? What best describes your project: <b>Single object with fields (e.g., “Todo” with ID, name, description)</b>
? Do you want to edit the schema now? <b>No</b>
</pre>

Though we choose ToDo and we don't edit the GraphQL schema here, we will be editing below with the correct values for our application.

<pre>
? Do you want to edit your newly created model? <b>Yes</b>
Please edit the file in your editor: <b>unicornflix/amplify/backend/api/unicornflix/schema.graphql</b>
</pre>

Navigate to the file schema.graphql located at unicornflix/amplify/backend/api/unicornflix/schema.graphql using the Cloud9 file explorer on the left hand side panel, and double click schema.graphql file to open it. We are going to edit the schema to remove the Todo model that was added earlier by the default API generation. **Do not click enter until in the terminal until the schema has been modified and the file has been saved**

The new schema should look like this if you removed just the Todo model:

```graphql
type vodAsset @model (subscriptions: {level: public})
@auth(
  rules: [
    {allow: groups, groups:["Admin"], operations: [create, update, delete, read]},
    {allow: private, operations: [read]}
  ]
)
{
  id:ID!
  title:String!
  description:String!

  #DO NOT EDIT
  video:videoObject @connection
} 

#DO NOT EDIT
type videoObject @model
@auth(
  rules: [
    {allow: groups, groups:["Admin"], operations: [create, update, delete, read]},
    {allow: private, operations: [read]}
  ]
)
{
  id:ID!
}
```

<pre>
? Press enter to continue 

GraphQL schema compiled successfully.

Edit your schema at unicornflix/amplify/backend/api/unicornflix/schema.graphql or 
place .graphql files in a directory at unicornflix/amplify/backend/api/unicornflix/schema

</pre>
