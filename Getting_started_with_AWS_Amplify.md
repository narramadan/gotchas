# Getting started with AWS Amplify with React application

## Install & Initialize Amplify in React application
* Install AWS Amplify CLI
```
$ npm install -g @aws-amplify/cli
```
* Install Create react app CLI
```
$ npm install -g create-react-app
```
* Create react project
```
$ create-react-app aws-amplify-test

$ cd aws-amplify-test
```
* Install nodejs packages for AWS Amplify
```
$ npm install aws-amplify aws-amplify-react
or
$ yarn add aws-amplify aws-amplify-react
```
* Initialize Amplify 
```
$ amplify init
```
* Accept defaults and provide values to those you wish to have as part of initializing amplify environment

## Add Authetication capability
* Add AWS Cognito Authentication capability 
```
$ admplify add auth
```
* Choose option to configure manually and enter resouce name as `amplifytestcognitouserpool` and pool name as `amplify_test_cognitouserpool`
* Choose rest of the options as per authetication requirements
* Include amplify library and configuration code as below to setup Authetication in app.js
```
import Amplify from 'aws-amplify';
import awsmobile from './aws-exports';
import { withAuthenticator } from 'aws-amplify-react';
Amplify.configure(awsmobile);
....
....
....
export default withAuthenticator(App, true);
```
* Check Amplify Status
```
$ amplify status

should return something as below

Current Environment: dev

| Category | Resource name              | Operation | Provider plugin   |
| -------- | -------------------------- | --------- | ----------------- |
| Auth     | amplifytestcognitouserpool | Create    | awscloudformation |
```
* Push changes
```
$ amplify push
```
* Login to AWS console and check if `amplify_test_cognitouserpool-dev` user pool is created in Cognito. `-dev` is appended as we used `dev` as the environment when initializing amplify
* Start React application
```
$ npm start
or
$ yarn start
```
* Accessing `http://localhost:3000/` should show up default login screen provided by AWS Cognito
* Signup with your username, password, email and phone number
* Check your mobile/email for the verification code. If you haven't received, confirm the user manually from AWS Cognito console
* Login with the username and password
* should be routed to home page with logout button displayed in the header

## Add GraphQL API
* Run below command to add API and choose `GraphQL`
```
$ amplify add api
```
* Choose name `amplifyTestAPI`
* Choose Cognito authetication type
* Choose `No` for annotated GraphQL schema
* Choose `Yes` for guided schema creation
* Choose `One-to-many relationships` for project
* Choose `Yes` to edit the schema now. This will create `amplify\backend\api\amplifyTestAPI\schema.graphql` and open it in VS Code editor
```
type Blog @model {
  id: ID!
  name: String!
  posts: [Post] @connection(name: "BlogPosts")
}
type Post @model {
  id: ID!
  title: String!
  blog: Blog @connection(name: "BlogPosts")
  comments: [Comment] @connection(name: "PostComments")
}
type Comment @model {
  id: ID!
  content: String
  post: Post @connection(name: "PostComments")
}
```
* Press enter to end the schema creation
* Check Amplify Status
```
$ amplify status

should return something as below

Current Environment: dev

| Category | Resource name              | Operation | Provider plugin   |
| -------- | -------------------------- | --------- | ----------------- |
| Api      | amplifyTestAPI             | Create    | awscloudformation |
| Auth     | amplifytestcognitouserpool | No Change | awscloudformation |
```
* Push the changes
```
$ amplify push
```
* When prompted for code generation, choose `Yes` and accept defaults for subsequent prompts
* This should display the GraphQL endpoint when all the resources are created/updated in the cloud
* As part of the API creation in cloud, you can observe there are bunch of folders & files created under `amplify\backend\api` and `src\graphql`
* Schema is for a Blog application where we can create blogs and manage posts and comments under them.
* As we can see, type `Blog` has reference to type `Post` and type has the same vice-versa. And this applies the same to type `Post` and `Comment`.
* Refer to [Amplify Docs](https://aws-amplify.github.io/docs/cli/graphql?sdk=js#api-category-project-structure) for the project structure created for the API
* Go to AWS Console > Appsync and see the API is created with suffix `-dev` appened to it.
* Click on the API name to through Schema, datasource that is created based upon schema
* DynamoDB Table created under this API will include the API Id in the table name. This will ensure that different tables are created for different Amplify environments
* To play with the schema from Queries section, get the `aws_user_pools_web_client_id` from `src\aws-exports.js`. Click on Login via Cognito User Pool. Provide the client id and user credentials that is provided during user signup as above.
* Click on `< Docs` and choose the appropriate option to use the GraphQL Playground app
* Sample to create a blog
```
// Execute below query to perform mutation to create new blog
mutation CreateReviewForEpisode($blog: CreateBlogInput!) {
  createBlog(input: $blog) {
    id
    name
  }
}

// Under Query Variables
{
  "blog": {
    "name": "First Blog"
  }
}

// This should return something like below once blog is created
{
  "data": {
    "createBlog": {
      "id": "d322a73a-17c3-48cf-911a-a549e3f94353",
      "name": "First Blog"
    }
  }
}
```
* Sample to query
```
// List all blogs with posts under it
{
	listBlogs {
    items {
      id
      name
      posts {
        items {
          id
          title
          blog {
            name
          }
        }
      }
    }
  }
}
```

## Use GraphQL API in React app
* Update App.js with the below which will create a blog with unique name and list all blogs that are created.
```
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

import Amplify, {API, graphqlOperation} from 'aws-amplify';
import awsmobile from './aws-exports';
import { withAuthenticator } from 'aws-amplify-react';

import uuid4 from 'uuid4'

import {listBlogs} from './graphql/queries'
import {createBlog} from './graphql/mutations'

Amplify.configure(awsmobile);

class App extends Component {

  createBlogMutation = async() => {
    console.log('Creating Blog');
    const CreateBlogInput = {
      name: 'Blog-'+uuid4()
    };

    const newEvent = await API.graphql(graphqlOperation(createBlog, {
      input: CreateBlogInput
    }));
    console.log('Blog is created: ',JSON.stringify(newEvent));
  }

  listBlogsQuery = async() => {
    console.log('listing blogs');
    const allBlogs = await API.graphql(graphqlOperation(listBlogs));
    console.log('Available blogs:', JSON.stringify(allBlogs));
  }

  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <span>
            <button onClick={this.createBlogMutation}>Create new Blog</button>
            <button onClick={this.listBlogsQuery}>List all blogs</button>          
          </span>
        </header>
      </div>
    );
  }
}

export default withAuthenticator(App, true);
```
* Login to the application
* Open up developer console and click on Create new blog & List all blogs and see up the magic !!!

## Add Analytics Capability
* Run below command to add Analytics capabilities and name it `awsamplifytest`
```
$ amplify add analytics
```
* Choose `No` when prompted when asked for allow guests and unautheticated users
* Running `amplify status` should show something like below
```
λ amplify status

Current Environment: dev

| Category  | Resource name              | Operation | Provider plugin   |
| --------- | -------------------------- | --------- | ----------------- |
| Analytics | awsamplifytest             | Create    | awscloudformation |
| Auth      | amplifytestcognitouserpool | Update    | awscloudformation |
| Api       | amplifyTestAPI             | No Change | awscloudformation |
```
* Run `amplify push` to create `pinpoint` service. It should show up  `All resources are updated in cloud`
* Add the below code to App.js which will publish events when user clicks add blog and list all blog button. Actually click these couple of times.
```
import Amplify, {API, graphqlOperation, Analytics} from 'aws-amplify';
....
....

createBlogMutation = async() => {
....
....
Analytics.record('Blog is created');
}

listBlogsQuery = async() => {
....
....
Analytics.record('listing blogs');
}
```
* Login to aws console and select service `Pinpoint`
* Click on the service created with `-dev` and navigate to `Analytics > Events`. Click on `Event` dropdown and you will see the events that we actually fired in the above code and you can see the number of times the event occurred is number of times you clicked the button.

## Pagination
#TODO# - Yet to do

## Using `@auth` directive
Follow the below steps to protect adding/updating type `Blog` with `@auth` directive.
#TODO# - Yet to do

## Adding Storage Capability
Lets add capability to write/read documents from S3
#TODO# - Yet to do

## Host the App using Amplify
* Run below command to add host the app on Amazon S3.
```
$ amplify add hosting
```
* Choose `Dev` when prompted for environment
* Choose default for hosting bucket name, index doc, error doc
* Running `amplify status` should show something like below
```
Current Environment: dev

| Category  | Resource name              | Operation | Provider plugin   |
| --------- | -------------------------- | --------- | ----------------- |
| Hosting   | S3AndCloudFront            | Create    | awscloudformation |
| Auth      | amplifytestcognitouserpool | No Change | awscloudformation |
| Api       | amplifyTestAPI             | No Change | awscloudformation |
| Analytics | awsamplifytest             | No Change | awscloudformation |
```
* Run `amplify publish` to publish the application on S3.
* You should see the message that app is successfully hosted with the url looking something like this - http://aws-amplify-test-XXXXXXXXXX-hostingbucket-dev.s3-website-us-east-1.amazonaws.com
* Login and follow the steps done before to click tist blogs and create blog.

## Configure environment for Production
So far so good. Now its time to move the app to production.
* Lets create production environment by running below command
```
$ amplify env add
```
* Add env as `prod` and accept defaults for the rest of the questions
* Amplify will switch to the newly created environment by default. Run the below command to see the list of environments and what is selected by default
```
$ amplify env list
```
* This should display as below
```
$ amplify env list

| Environments |
| ------------ |
| dev          |
| *prod        |
```
* To switch to `dev` environment, run the below command
```
$ amplify env checkout dev
```
* You should see the environment is initialized successfully. Now switch back to prod using above command.
* Running `amplify status` should show that all resources that are created in dev environment are to be created in the prod environment
```
Current Environment: prod

| Category  | Resource name              | Operation | Provider plugin   |
| --------- | -------------------------- | --------- | ----------------- |
| Auth      | amplifytestcognitouserpool | Create    | awscloudformation |
| Api       | amplifyTestAPI             | Create    | awscloudformation |
| Analytics | awsamplifytest             | Create    | awscloudformation |
| Hosting   | S3AndCloudFront            | Create    | awscloudformation |
```
* Run `amplify push` and choose options that were selected when adding Auth, API, Analytics & Hosting and wait for the resources to be created.
* This will create all the resources and list you the endpoints for Pinpoint, GraphQL & Hosting something like below
```
√ Generated GraphQL operations successfully and saved at src\graphql
√ All resources are updated in the cloud

Pinpoint URL to track events https://console.aws.amazon.com/pinpoint/home/?region=us-east-1#/apps/XXXXXXXXc8ae6090db9a7bffd6/analytics/events
GraphQL endpoint: https://XXXXXXi3kufolm2qnfu.appsync-api.us-east-1.amazonaws.com/graphql
Hosting endpoint: http://aws-amplify-test-XXXXXXX-hostingbucket-prod.s3-website-us-east-1.amazonaws.com
```

## Configure Git for multi user development
Lets configure Git and have the code committed to Git Repo. I opted to host the app on Github, but we can go with any vendor.
* Create a repo and follow the series of steps to initialize Git and commit the code to the repo
```
$ git init

$ git add *

$ git commit -m "Initial Commit"

$ git remote add origin https://github.com/XXXXXX/aws-amplify-react-test.git

$ git push -u origin master
```
* This should now push the changes the code to repo that is created.
* Pass it to the team for them to use the repo to create additional APIs or work on app and push the changes to their desired environment.

## Configure CI/CD Pipeline to push & deploy changes to production
`Amplify Console` will enable to continiously deploy updates whenever their is a commit when the app is built with `Amplify`.

* Login to AWS and choose `AWS Amplify` which will open up the console.
* Click on `Connect app` button
* Select `Github` or the repo you are opted for and click next
* Authroize AWS Amplify to access the repositories from Github and choose the repository that should be added.
* Select the branch which should be monitoried for any commits and click next
* Choose the amplify environment that should be used by amplify console to deploy the changes. I select `prod` which is ideal case
* Click on `Create new role` and choose the appropriate permissions for this role.
* Choose the role that is created from the dropdown
* Click next. Review the changes and proceed by clicking `Save & deploy`.
* Wait for `master` branch to be provisioned, built, deployed and finally verified which will finally lead to every stage in green color.
* Click on the link displayed below the app screenshot which would open the deployed app.
* As we didn't test Prod environment when it is deployed with new resources, we need to signup before we can test GraphQL and Pinpoint.
* Upon signingup, Login to the application and test by clicking the buttons as before. Verify the developer console and pinpoint for events that are published.

## Add Custom resolvers
As mentioned in [Amplify Docs](https://aws-amplify.github.io/docs/cli/graphql?sdk=js#add-a-custom-resolver-that-targets-a-dynamodb-table-from-model), if we need to write specific queries we need write custom resolvers.

If we observe `src\graphql\queries.js`, we see there are only six queries generated. `getBlog`, `ListBlogs`, `GetPost`, `listPosts`, `GetComment` and `ListComments`. But these will not suffice our needs to fetch all posts under a specific blog or fetch all comments under a speific post.

Follow the below steps to create custom resolvers for two queries `postsForBlog` when blog id is passed and `commentsForPost` when post if is passed.
* Add the below code to `amplify\api\amplifyTestAPI\schema.graphql` to add additional types and queries
```
type Posts {
  items: [Post]
  nextToken: String
}

type Comments {
  items: [Comment]
  nextToken: String
}

type Query {
  # Fetch posts for a specific blog
  postsUnderBlog(blogId: ID!, limit: Int, nextToken: String): Posts

  # Fetch comments for a specific post
  commentsUnderBlog(postId: ID!, limit: Int, nextToken: String): Comments
}
```
* Add the below resolvers for the queries that are added as above under `amplify\api\amplifyTestAPI\resolvers`

#`Resolver`# is written in [Apache Velocity Template Language](http://velocity.apache.org/engine/1.7/user-guide.html), which takes request as input and outputs json document. Instructions on how to get the data, transform or apply complex logic such as looping through arguments before inserting data to DynamoDB or fetching data from multiple columns and map them to a single field when returning back.

Refer to [Appsync Resolver Mapping Template](https://docs.aws.amazon.com/appsync/latest/devguide/resolver-mapping-template-reference-overview.html) document for overview on how to implement resolvers.

`Query.postsUnderBlog.req.vtl`
```
#**
# Resolver to fetch posts under specific blog
*#
#set( $limit = $util.defaultIfNull($context.args.limit, 10) )
{
  "version": "2017-02-28",
  "operation": "Query",
  "query": {
    "expression": "#connectionAttribute = :connectionAttribute",
    "expressionNames": {
        "#connectionAttribute": "postsBlogId"
    },
    "expressionValues": {
        ":connectionAttribute": {
            "S": "$context.args.blogId"
        }
    }
  },
  "scanIndexForward": true,
  "limit": $limit,
  "nextToken": #if( $context.args.nextToken ) "$context.args.nextToken" #else null #end,
  "index": "gsi-BlogPosts"
}
```
`Query.postsUnderBlog.res.vtl`
```
$util.toJson($ctx.result)
```

`Query.commentsUnderBlog.req.vtl`
```
#TODO#
```
`Query.commentsUnderBlog.res.vtl`
```
#TODO#
```
* Add the resolver resource to the stack by modifying `amplify\api\amplifyTestAPI\stacks\CustomResource.json` under `Resources`
```json
"QueryPostsUnderBlogResolver":{  
   "Type":"AWS::AppSync::Resolver",
   "Properties":{  
      "ApiId":{  
         "Ref":"AppSyncApiId"
      },
      "DataSourceName":"PostTable",
      "TypeName":"Query",
      "FieldName":"postsUnderBlog",
      "RequestMappingTemplateS3Location":{  
         "Fn::Sub":[  
            "s3://${S3DeploymentBucket}/${S3DeploymentRootKey}/resolvers/Query.postsUnderBlog.req.vtl",
            {  
               "S3DeploymentBucket":{  
                  "Ref":"S3DeploymentBucket"
               },
               "S3DeploymentRootKey":{  
                  "Ref":"S3DeploymentRootKey"
               }
            }
         ]
      },
      "ResponseMappingTemplateS3Location":{  
         "Fn::Sub":[  
            "s3://${S3DeploymentBucket}/${S3DeploymentRootKey}/resolvers/Query.postsUnderBlog.res.vtl",
            {  
               "S3DeploymentBucket":{  
                  "Ref":"S3DeploymentBucket"
               },
               "S3DeploymentRootKey":{  
                  "Ref":"S3DeploymentRootKey"
               }
            }
         ]
      }
   }
}
```
* Compile graphql and see if the changes done till this point doesnt have any errors
```
$ amplify api gql-compile
```
#TODO# - Testing

* Modify `amplify\api\amplifyTestAPI\stacks\CustomResource.json` to add resources for the resolvers that are created 

## Update GraphQL Schema by adding non-null field to existing type which has DynamoDB table already created with data in it
* Lets update the schema for type `Blog` to add not-null type `Category` which is an enum
* Swicth to dev environment by running below command
```
$ amplify env checkout dev
```
* Update schema as below in `amplify\backend\api\amplifyTestAPI\schema.graphql`
```
type Blog @model {
  id: ID!
  name: String!
  posts: [Post] @connection(name: "BlogPosts")
  category: Category!
}
type Post @model {
  id: ID!
  title: String!
  blog: Blog @connection(name: "BlogPosts")
  comments: [Comment] @connection(name: "PostComments")
}
type Comment @model {
  id: ID!
  content: String
  post: Post @connection(name: "PostComments")
}

enum Category {
  Technology
  Science
  Politics
  Books
}
```
* Compile GraphQL once the schema is updated to verify if there are any compilation issues
```
$ amplify api gql-compile
```
* Now check for amplify status, we will see `API` is changed and needs an `Update` as below
```
$ amplify status

Current Environment: dev

| Category  | Resource name              | Operation | Provider plugin   |
| --------- | -------------------------- | --------- | ----------------- |
| Api       | amplifyTestAPI             | Update    | awscloudformation |
| Auth      | amplifytestcognitouserpool | No Change | awscloudformation |
| Analytics | awsamplifytest             | No Change | awscloudformation |
| Hosting   | S3AndCloudFront            | No Change | awscloudformation |
```
* Push the changes and accept with `Y` when prompted for update code & GraphQL statements generation
```
$ amplify push
```
* Modify the code to include `Category` when creating the `Blog` as below in `app.js`
```
#TODO# : Getting Errors
```
## Using Lambda Functions
Lets notify all authenticated users when there is a new post is created
#TODO# - Yet to do

## Delete Amplify resources
Delete all AWS resources that are created for specific environent
#TODO# - Yet to do

## References
* [GraphQL Schema Definition Language](https://facebook.github.io/graphql/June2018/)
* [When to use GraphQL Non-null fields](https://medium.com/@calebmer/when-to-use-graphql-non-null-fields-4059337f6fc8)
