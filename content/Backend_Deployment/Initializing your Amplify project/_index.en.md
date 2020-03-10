+++
title = "Initializing your Amplify Project"
date = 2020-03-09T12:03:35-07:00
weight = 5
chapter = true
pre = "<b>1. </b>"
+++

1. First, we need to change directories to the root folder of our project.
    * `cd UnicornFlix`
1. Next we are going to begin development of our Amplify project by using the initialization command.  This command creates new AWS backend resources (in this case a single S3 bucket to host your CloudFormation templates) and pulls the AWS service configurations into the app!
    * `amplify init`
1. Follow the prompts shown below.
    * **PLEASE DOUBLE CHECK THE PROFILE YOU ARE USING.**
    * Note that because of the services leveraged, your AWS profile **MUST USE** us-west-2, us-east-1, eu-west-1, eu-central-1, ap-northeast-1, or ap-southeast-2.
    <pre>
    unicornflix $ <b>amplify init</b>
    
    Note: It is recommended to run this command from the root of your app directory
    ? Enter a name for the project: <b>unicornflix</b>
    ? Enter a name for the environment <b>dev</b>
    ? Choose your default editor: <b>None</b>
    ? Choose the type of app that you're building <b>javascript</b>
    Please tell us about your project
    ? What javascript framework are you using <b>react</b>
    ? Source Directory Path:  <b>src</b>
    ? Distribution Directory Path: <b>build</b>
    ? Build Command:  <b>npm run-script build</b>
    ? Start Command: <b>npm run-script start</b>
    Using default provider  <b>awscloudformation</b>

    For more information on AWS Profiles, see:
    https://docs.aws.amazon.com/cli/latest/userguide/cli-multiple-profiles.html

    ? Do you want to use an AWS profile? <b>Yes</b>
    ? Please choose the profile you want to use <b>default</b>
    </pre>