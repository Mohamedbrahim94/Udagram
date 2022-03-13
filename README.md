# Udacity Deployment project Udagram

This application is provided to you as an alternative starter project.The udagram application is a fairly simple application that includes all the major components of a Full-Stack web application.

## Getting Started
1. I have uploaded this project from my local machine to my Github repo udacity `https://github.com/Mohamedbrahim94/udagram` .
2. using git commands to add my updated codes.
3. Moving to my psql terminal creating my database `udagram` and connected my application to my database locally and ensure with postbird that is connected successfully locally and on AWS RDS.
4. Then moving to AWS console setting my services: ( IAM , RDS , S3 , Elasticbeanstalk ).

### statup setup

- Node v16.13.1 

- npm v8.1.2 

- python v3.7.9

- pip v20.1.1

- AWS CLI v2, aws-cli/2.4.21 python/3.8.8 windows/10 exe/AMD64 prompt/off

### Testing

This project contains two different test suite: unit tests and End-To-End tests(e2e). Follow these steps to run the tests.

1. `cd starter/udagram-frontend`
1. `npm run test`
1. `npm run e2e`

There are no Unit test on the back-end

### Unit Tests:

Unit tests are using the Jasmine Framework.

### End to End Tests:

The e2e tests are using Protractor and Jasmine.

## Built With

- [Angular](https://angular.io/) - Single Page Application Framework
- [Node](https://nodejs.org) - Javascript Runtime
- [Express](https://expressjs.com/) - Javascript API Framework

### Architecture Diagram 
 I have created a diagram using `lucidchart` to show an overview of my application infrastructure to be deployed
this diagram will found at Screenshots `Docs` in the root directory. `docs\Architecture diagram.png`

### Installation
Provision the necessary AWS services needed for running the application:
1. In AWS, provision a publicly available RDS database running Postgres. `<https://console.aws.amazon.com/rds/home?region=us-east-1#database:id=udagram-1;is-cluster=false>`
>>RDS ENDPOINT : `udagram-1.cv6dxmbvcdcf.us-east-1.rds.amazonaws.com`

2. In AWS, provision a s3 bucket for hosting the uploaded files. 
 S3 endpoint `http://udagrambucketpj3.s3-website-us-east-1.amazonaws.com`

3. Export the ENV variables needed or use a package like [dotnev](https://www.npmjs.com/package/dotenv)/.

4. From the root of the repo, navigate backend `cd udagram` then `cd udagram-api` to install the node_modules `npm install`. After installation use `npm run build` and to start locally use `npm run dev`.

5.  From the root of the repo, navigate backend `cd udagram` then `cd udagram-frontend` to install the node_modules `npm install`. After installation use `npm run build` and to start locally use `npm run start`.

6. Circleci last build check : `docs\CircleCi\Pipelines -Last_build_udagram -.png`

7. elasticbean app health check : `docs\ElasticBeanStalk\Udagram-env - health.png`

### Automation deployment:
#### FrontEnd locally
  
  1. Build script is added to package.json and run command with : `npm run build`.
  2. www directory containing `index.html` which is static host file which will be uploaded to AWS S3 bucket.
  3. Creating `bin` directory add a `deploy.sh` file which have `automated script` to deploy frontend build to AWS S3 bucket `udagrambucketpj3`
  4. Adding deploy script to package.json used automation to deploy frontend which read command from `bin/deploy.sh` file.  

#### Backend locally

  1. build script is added to package.json run with command `npm run build` which will create a `www` directory including `Archive.zip` file
  which will the file to be uploaded to AWS elasticbeanstalk to deploy udagram application api.
  2. Creating `bin` directory containing `deploy.sh` file used for setting `elasticbeanstalk-environment` and `environment variables` locally to be used in automated deployment.
  4. adding deploy script in package.json used automation command to deploy backend to `elasticbeanstalk` with `env-settings` in `bin/deploy.sh` file.
  5. `.env` file has been created adding environment variables in it.
    
    add the following environments variables in `.env` file 
``
POSTGRES_HOST=udagram-1.cv6dxmbvcdcf.us-east-1.rds.amazonaws.com  >> `RDS endpoint/host`
BD_PORT=5432
PORT=3000
POSTGRES_PASSWORD=H2Tw5xtZj52tsyUOuLax
POSTGRES_USERNAME=postgres
RDS_DIALECT=postgres
POSTGRES_DB=postgres
AWS_REGION=us-east-1
AWS_PROFILE=default
AWS_BUCKET=udagrambucketpj3
URL=http://localhost
AWS_ACCESS_KEY_ID=AKIARTZIX75CISTXCMYJ
AWS_SECRET_ACCESS_KEY=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
JWT_SECRET=me-mohibrahim-secret

``

### Screenshots provided
 Please check Screenshoot directory `/docs` in the root directory which includes : 

1. docs\Architecture Diagram : Application infrastructure diagram 
2. docs\CircleCi : includes last build of my circleci which has been succeded.
3. docs\ElasticBeanStalk : All steps to be included for setting aws elasticbeanstalk for my quoteapp application.
4. docs\IAM : Steps for creating aws user in details showing my USER ACCESS ID KEY and USER ACCESS SECRET ID.
5. docs\RDS : steps for creating a database for my application using amazon web services.
6. docs\S3 : steps for creating S3 bucket for my application.
7. docs\Terminal : shows some commands used in my terminal regarding versions , configuring AWS and deploying app using elasticbeanstalk. 

### Endpoints
  1. API Host/Endpoint link : `http://udagram-env.eba-dtvs3jet.us-east-1.elasticbeanstalk.com` 
      There's a screenshot of the api host founds in `docs` directory  :
      `docs\ElasticBeanStalk\Elasticbean host .png`

  2. Static host/endpoint link : `http://udagrambucketpj3.s3-website-us-east-1.amazonaws.com`
      There's a screenshot of the api host founds in `Screenshot` directory  :
       `docs\S3\S3 bucket ENDPOINT.png`

  3. AWS RDS endpoint : `udagram-1.cv6dxmbvcdcf.us-east-1.rds.amazonaws.com`.

 Automated EB Cli documentation will be found below in the `elasticbeanstalk` section.

### Manual deployment to Amazon web services (AWS): 

1. Launch AWS console provided
2. Creating a user using `AWS IAM`. 
3. Creating a postgres database using `AWS RDS`. >> for all steps details please check
4. Creating a simple storage bucket using `AWS S3`
5. Creating elasticbeanstalk app `udagram` with `Udagram-env`

#### AWS IAM 
 created a user and gives it `FullAdministatorAccess`
- for all steps details please check : `docs\IAM`
1. Account ID: 1112-1773-7540
2. username : mohamed-pj3
3. USER ACCESS ID KEY : AKIARTZIX75CISTXCMYJ
4. USER ACCESS SECRET ID : 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
 

#### AWS RDS 
 Created a `udagram-1` database for my application with RDS Master username `postgres` and Master Password `H2Tw5xtZj52tsyUOuLax`

- AWS RDS endpoint : `udagram-1.cv6dxmbvcdcf.us-east-1.rds.amazonaws.com`
- in my `.env` file set :
   DB_HOST=`udagram-1.cv6dxmbvcdcf.us-east-1.rds.amazonaws.com` 
   DB_PORT=`5432`  
- for all steps details please check : `docs\RDS`

 After creating a IAM user and give it all admin access sign in to AWS console with :
1. Account ID: 1112-1773-7540
2. username : mohamed-pj3
3. USER ACCESS ID KEY : AKIARTZIX75CISTXCMYJ
4. USER ACCESS SECRET ID : 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


#### AWS S3 
>> created a simple storage bucket named `udagrambucketpj3` for my application 
1. setting  my `AWS S3 Bucket Policy ` in permission section.
2. used it in my `frontend/bin/deploy.sh` file for uploading app build from `www` directory to my `AWS S3 bucket ` udagrambucketpj3   
3. S3 host : `http://udagrambucketpj3.s3-website-us-east-1.amazonaws.com`
- for all steps details please check : `docs\S3`

#### ElasticbeanStalk 
>> created an app named `udagram` with environment `Udagram-env` using `AWS Elasticbean`
1. setting my application name and choose platform and version `Node.js 14 running on 64bit Amazon Linux 2`
2. Navigating to environment configurations and adding my environment variables 
3. checking health of my app to be OK for any issues check `logs`
4. eb endpoint - api host : `http://udagram-env.eba-dtvs3jet.us-east-1.elasticbeanstalk.com/`
- for detailed steps please check : `docs\ElasticBeanStalk`

- Also you can configure elasticbean stalk and deploy the application using automated scripts and commands.
 >> lanuch terminal:
   1. configure aws 
   2. check python/pip version if not installed please install it check documentations below to do so 
   3. check aws-cli version check documentations below `use intallation command to install it `
   4. use command `eb init`
   5. `.elasticbean` directory will be created or create it manually in the root directory
   5. add in it `config.yml` file and add elasticbean configuration :
  ``
   branch-defaults:
  master:
    environment: <elasticbeanstalk:environment-name>
 global:
  application_name: <Application Name>
  default_ec2_keyname: <elasticbeanstalk:environment-id>
  default_platform: <platform name>
  default_region: <AWS region>
  sc: git
  ``
6. use command : `eb init --platform <Node.js> --region <us-east-1> <udagram>`.
7. Start by connecting the EB CLI to the environment with command : `eb use Udagram-env`
8. Save the attached environment's current configuration: `~/project$ eb config save --cfg quoteapp-v1`
9. Modify the saved configuration locally if needed.
10. Upload the saved configuration to S3: `eb config put udagram-v1`
11. Identify your Elastic Beanstalk environment's environment ID with describe-environments:`aws elasticbeanstalk describe-environments --environment-name Udagram-env`
12. Check the health of the environment with the : `eb health` 
13. to clean or delete use command : `eb terminate`
14. f you see that the health is not indicating an "OK" status, use the command  `eb logs`
15. When environment creation completes, use the `eb open`

>> To set up a Git repository commands : 
1. `git init`
2. `git commit -m "First express app"`
3. `eb deploy`
4. `git add .ebextensions/ app.js`
5. `git commit -m "Serve stylesheets statically with nginx."`

>> For detailed steps please check : 
1. `docs\Terminal\aws configurations terminal.png`
2. `docs\ElasticBeanStalk\eb commands in terminal.png`
3. `docs\ElasticBeanStalk\eb creating sample app.png`
####  set up AWS security access for CircleCI

1. navigate back to the AWS management console and select Identity and Access Management
2. select Users in the left menu bar, then click on add user
3. enter any name you want and check the "programatic access" checkbox

#### set up AWS security access for CircleCI
1. Navigate back to your Circle CI page and select the organization with your project then click on the settings icon on the left. Click on the context option then "create context".
2. I am choosing the name aws to match the context specified in my .circleci/config.yml file in the workflows section.
3. Click on the newly created context and add two new variables.
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
4. Enter in the value of these variables from the credentials.csv file downloaded in the previous step.


#### Continuous integration and Pipeline using `Circleci`:
 1. Creating package.json file in the root directory adding automated scripts for continuous integration to Circleci
 2. Creating `.circleci` directory containing `config.yml` file adding in it `circleci configuations` for `CI/CD` 
 3. Navigating to `CircleCi dashboard` after connecting it to my `Github`.
 4. Opening my project to be deployed and setting `configuration` for deploying from my `config.yml` file 
 5. Navigating to project setting and adding my environments variables for `AWS` as shown in `docs\CircleCi\Circleci Environment Variables - udagram -.png`and ``
 6. Circleci last build check : `docs\CircleCi\Pipelines -Last_build_udagram -.png`

 #### Package.Json
 1. Angular/cli is added as devdependencies 
- All steps are shown in [Screenshots\CircleCi] 
2. scripts for CI/CD is added 

#### aws configure 
- please check : `docs\Terminal\aws configurations terminal.png` 
commands used in terminal : 
`aws configure` >> 
1. AWS Access Key ID [****************CMYJ]: my key-ID
2. AWS Secret Access Key [****************FO4q]: my Secret Access key
3. Default region name [us-east-1]: used default for me
4. Default output format [json]: json


#### Documentations used : 

#### AWS CLI
[AWS CLI DOCS](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

#### Configure AWS CLI
[DOCS](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

#### EB CLI

####  Installation
  - [EB CLI Windows](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-windows.html)
  - [Install Pyhthon 3.7.x](https://www.python.org/downloads/windows/)

#### Guide
[EB CLI DOCS](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-getting-started.html)

[Setting configuration EB] (https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environment-configuration-methods-before.html)

