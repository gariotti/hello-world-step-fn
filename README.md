# Serverless Localstack 
## ARCHIVED 
This repo has been merged into https://github.com/aligent/serverless-aws-nodejs-service-template

## Introduction
A Typescript stepfunction template with a docker based LocalStack development environment.  

## Setup
Add localstack credentials block to ~/.aws/credentials (creds don't matter)

```
[localstack]
aws_access_key_id = localstack
aws_secret_access_key = localstack
```

Add localstack profile block to ~/.aws/config
```
[profile localstack]
region = ap-southeast-2
output = json
```

### Local NPMDeploy the serverless stack
`npm run deploy-local`

Invoke the step function
`npm run invoke-local-stepf helloWorld`

Invoke the step function with data
`npm run invoke-local-stepf helloWorld --data='{}'`

Invoke the step function with json file
`npm run invoke-local-stepf helloWorld --path='input.json'`

Invoke individual lambdas
`npm run invoke-local hello`

Invoke individual lambdas with data
`npm run invoke-local hello --data='{}'`

Invoke individual lambdas json file
`npm run invoke-local hello --path='input.json'`

### Aliased NPM

Add the following to your `.bashrc` file:

```
alias node-run='docker run --rm -it --volume ~/.aws:/home/node/.aws --volume ~/.npm:/home/node/.npm --volume $PWD:/app aligent/serverless'
alias serverless='node-run serverless'
alias sls-deploy-local='docker-compose exec -u node -w /app offline /serverless/node_modules/serverless/bin/serverless.js deploy --log --profile localstack --stage dev'
alias sls-invoke='docker-compose exec -u node -w /app offline /serverless/node_modules/serverless/bin/serverless.js invoke --log --profile localstack --stage dev --function'
alias sls-invoke-stepf='docker-compose exec -u node -w /app offline /serverless/node_modules/serverless/bin/serverless.js invoke stepf --log --profile localstack --stage dev --name'
```

You will then need to reload your bashrc file, either by running `. ~/.bashrc` or starting a new terminal session.

Then install dependencies with `node-run npm install`.

## Usage

Start Localstack
`docker-compose up`

### Local NPM
Deploy the serverless stack
`npm run deploy-local`

Invoke the step function
`npm run invoke-local-stepf helloWorld`

Invoke the step function with data
`npm run invoke-local-stepf helloWorld --data='{}'`

Invoke the step function with json file
`npm run invoke-local-stepf helloWorld --path='input.json'`

Invoke individual lambdas
`npm run invoke-local hello`

Invoke individual lambdas with data
`npm run invoke-local hello --data='{}'`

Invoke individual lambdas json file
`npm run invoke-local hello --path='input.json'`

### Aliased NPM
Deploy the serverless stack
`sls-deploy-local`

Invoke the step function
`sls-invoke-stepf helloWorld`

Invoke the step function with data
`sls-invoke-stepf helloWorld --data='{}'`

Invoke the step function with json file
`sls-invoke-stepf helloWorld --path='input.json'`

Invoke individual lambdas
`sls-invoke hello`

Invoke individual lambdas with data
`sls-invoke hello --data='{}'`

Invoke individual lambdas json file
`sls-invoke hello --path='input.json'`
