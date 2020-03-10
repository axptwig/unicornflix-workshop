+++
title = "Pushing your local project to AWS"
date = 2020-03-09T12:03:35-07:00
weight = 15
chapter = true
pre = "<b>3. </b>"
+++

1. Once the prompts complete, make sure the module was added by checking the project status.
    * `amplify status`
<pre>
unicornflix $ <b>`amplify status`</b>

Current Environment: <b>dev</b>

| Category | Resource name       | Operation | Provider plugin   |
| -------- | ------------------- | --------- | ----------------- |
| <b>Auth</b>     | <b>unicornflix1e7c3699</b> | Create    | awscloudformation |
| <b>Auth</b>     | <b>userPoolGroups</b>      | Create    | awscloudformation |
| <b>Api</b>      | <b>unicornflix</b>         | Create    | awscloudformation |
| <b>Video</b>    | <b>unicornflix</b>         | Create    | awscloudformation |

</pre>
Now it is time to actually create the resources by pushing the configuration to the cloud. 

1. Run amplify push to create the backend video resource which is comprised of the services necessary to manage, process, and serve our videos. We'll need to answer a few questions to generate code for interacting with GraphQL from our application, which will be used later in our development.
    * `amplify push`

<pre>
unicornflix $ <b>amplify push</b>
? Do you want to generate code for your newly created GraphQL API <b>Yes</b>
? Choose the code generation language target <b>javascript</b>
? Enter the file name pattern of graphql queries, mutations and subscriptions <b>src/graphql/**/*.js</b>
? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions <b>Yes</b>
? Enter maximum statement depth [increase from default if your schema is deeply nested] <b>2</b>
</pre>
