## Accepting API Keys as a query string in Amazon API Gateway

This repository contains a sample [AWS SAM](https://aws.amazon.com/serverless/sam/) application which demonstrates how you can accept API Keys in [Amazon API Gateway](https://aws.amazon.com/api-gateway/) as query string parameters.

It's important to acknowledge that API keys are not a primary authorization mechanism for your APIs. If multiple APIs are associated with a usage plan, a user with a valid API key can access all APIs in that usage plan. We provide [numerous options](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-to-api.html) for securing access to your APIs, including [resource policies](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies.html), [Lambda authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html), and [Amazon Cognito user pools](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html).

This repository is accompanied by a [blog post](https://aws.amazon.com/blogs/compute/accepting-api-keys-as-a-query-string-in-amazon-api-gateway/) authored by Ronan Prenty & Zac Burns. 

## Pre-requisites
1. [Install the AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
2. [Configure the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

## Instructions
1. Clone this repository ```git clone https://github.com/aws-samples/amazon-apigateway-accept-apikeys-as-querystring.git```
2. Navigate locally to the repository using your command line
3. Execute the following code:
```
sam build 
// if you encounter Python version issue, use: sam build --use-container

sam deploy --guided
```
4. From the outputs, copy the URL and put it in your browser. 
![Alt text](diagrams/TemplateOutput.png?raw=true "Title")
## Architecture Diagram
![Alt text](diagrams/API_Keys.png?raw=true "Title")
### Walk through
1.	Client sends HTTP request to API with the API Key in the query string
2.	Amazon API Gateway sends the request to a REQUEST type custom authorizer
3.	The custom authorizer function extracts the API Key from the payload. It constructs the response object with the API Key as the value for the `usageIdentifierKey` property
4.	The response gets sent back to API Gateway for validation. 
5.	API Gateway validates the API Key against a usage plan. 
6.	If valid, proceed to the backend. 

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

