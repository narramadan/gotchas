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

## Add Analytics
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

## Configure CI/CD Pipeline to push & deploy changes to production

## Delete Amplify resources
