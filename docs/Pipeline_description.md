# Overview
This document describes our CI/CD process

### Git Flow

- Create a feature branch for your task
- Once its completed push to the remote repositorie and create a pull request to merge with master branch
- Once pull request is approved and your code is merged with the master branch a circleci pipeline will start 

### Checking pipeline
- Open circleci web page
- Open our oraganization
- Click on projects
- On prjects list click on the Pipelines for udacity-udagram project
- Find the pipeline related with our commit and wait for completion

### Pipeline description

Find pipeline config at .circleci/config.yml

All steps are using npm scripts avaiable on the package.json at the root folder.

## Orbs Used
- circleci/node@5.0.3: Node.js orb for installing Node.js and running npm commands.
- circleci/aws-elastic-beanstalk@2.0.1: AWS Elastic Beanstalk orb for deploying applications to Elastic Beanstalk.
- circleci/aws-cli@3.1.1: AWS CLI orb for interacting with AWS services.

## Jobs
Build Job
The build job is responsible for building the application.

- Docker Image: cimg/node:14.15
- Steps:
    1. Install Node.js using the node/install command.
    2. Checkout the code.
    3. Verify Node.js and npm versions.
    4. Install front-end dependencies using npm run frontend:install.
    5. Install API dependencies using npm run api:install.
    6. Run front-end linting using npm run frontend:lint.
    7. Build the front-end using npm run frontend:build.
    8. Build the API using npm run api:build.

Deploy Job
The deploy job is responsible for deploying the application to AWS Elastic Beanstalk.

- Docker Image: cimg/base:stable
- Steps:
    1. Install Node.js version 14.15 using the node/install command.
    2. Checkout the code.
    3. Set up AWS Elastic Beanstalk using eb/setup.
    4. Set up AWS CLI using aws-cli/setup.
    5. Deploy the application using a series of npm commands:
        - npm run frontend:install
        - npm run frontend:build
        - npm run frontend:deploy
        - npm run api:install
        - npm run api:build
        - npm run api:deploy

## Workflows
The udagram workflow defines the order of job execution.

- Jobs:
    1. build: Builds the application.
    2. hold: A manual approval step that requires approval before proceeding.
    3. deploy: Deploys the application to AWS Elastic Beanstalk.

The deploy job requires approval from the hold job, which ensures that the deployment is only executed after manual approval.