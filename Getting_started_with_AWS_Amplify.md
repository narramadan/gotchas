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
* Run command to add API and choose `GraphQL`
```
$ amplify add api
```
* Choose name `amplifyTestAPI`
* Choose Cognito authetication type
* Choose `No` for annotated GraphQL schema
* Choose `Yes` for guided schema creation
* Choose `One-to-many relationships` for project
* Choose `Yes` to edit the schema now. This will create `schema.graphql` and open it in VS Code editor
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

## Host the App using Amplify

## Configure environments for Dev, Staging & Production

## Configure Git for multi user development

## Configure CI/CD Pipeline to push & deploy changes to production

## Delete Amplify resources
