Prerequisites
-------------

Before we start, make sure you have the following:

1.  Sign up on [serverless.com](https://www.serverless.com/).

2.  Node.js and npm installed. You can download them from [nodejs.org](https://www.serverless.com/).

3.  Serverless Framework installed globally. Run the following command:

```
npm install -g serverless

```

1.  AWS IAM User credentials for deployment.

[](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-project-setup "Permalink")
----------------------------------------------------------------------------------------------------------------------------------------

Project Setup
-------------

### [](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-step-1-clone-the-project-repository "Permalink")

### Step 1: Clone the Project Repository

Clone the project repository from GitHub:

```
git clone https://github.com/ArjunMnn/aws-node-http-api-project-dev.git

```

### [](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-step-2-install-dependencies "Permalink")

### Step 2: Install Dependencies

Navigate to the project directory and install the required npm packages:

```
cd aws-node-http-api-project-dev
npm install

```

### [](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-step-3-configure-aws-credentials "Permalink")

### Step 3: Configure AWS Credentials

Run the following command to configure your AWS credentials:

```
serverless config credentials --provider aws --key YOUR_ACCESS_KEY --secret YOUR_SECRET_KEY

```

Replace `YOUR_ACCESS_KEY` and `YOUR_SECRET_KEY` with your AWS IAM User credentials.

[](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-serverless-configuration "Permalink")
---------------------------------------------------------------------------------------------------------------------------------------------------

Serverless Configuration
------------------------

The `serverless.yaml` file defines the AWS infrastructure for your serverless project. Open the `serverless.yaml` file and replace the placeholder values in the `provider` section with your specific AWS configuration.

```
provider:
  name: aws
  runtime: nodejs14.x
  region: YOUR_AWS_REGION
  iamRoleStatements:
    - Effect: Allow
      Action:
        - dynamodb:*
      Resource:
        - arn:aws:dynamodb:YOUR_AWS_REGION:YOUR_ACCOUNT_ID:table/KaamKaro

```

Replace `YOUR_AWS_REGION` and `YOUR_ACCOUNT_ID` with your AWS region and account ID.

[](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-serverless-functions "Permalink")
-----------------------------------------------------------------------------------------------------------------------------------------------

Serverless Functions
--------------------

The project consists of several functions, each handling specific API endpoints. The function code is in separate files in the `src` directory.

-   `hello.js`: Handles the root endpoint and returns a welcome message.

-   `kaamBharo.js`: Adds a new task to the DynamoDB table.

-   `kaamDikhao.js`: Retrieves all tasks from the DynamoDB table.

-   `kaamHatao.js`: Deletes a task from the DynamoDB table.

-   `kaamKhatamKaro.js`: Updates the completion status of a task in the DynamoDB table.

[](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-dynamodb-table "Permalink")
-----------------------------------------------------------------------------------------------------------------------------------------

DynamoDB Table
--------------

The `serverless.yaml` file includes a DynamoDB table definition. Ensure that you have the necessary permissions to create a DynamoDB table in your AWS account.

```
resources:
  Resources:
    KaamKaro:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: KaamKaro
        BillingMode: PAY_PER_REQUEST
        AttributeDefinitions:
          - AttributeName: id
            AttributeType: S
        KeySchema:
          - AttributeName: id
            KeyType: HASH

```

[](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-deploy-the-serverless-project "Permalink")
--------------------------------------------------------------------------------------------------------------------------------------------------------

Deploy the Serverless Project
-----------------------------

Run the following command to deploy the project to AWS:

```
serverless deploy

```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702199748384/57fea4a2-d7e6-4ac2-89d6-80989bb56854.png?auto=compress,format&format=webp)

This command will package and deploy your project using AWS CloudFormation.

[](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-testing-with-postman "Permalink")
-----------------------------------------------------------------------------------------------------------------------------------------------

Testing with Postman
--------------------

Use [Postman](https://www.postman.com/) to test your APIs. Here are some sample requests:

-   **GET /:** Retrieve a welcome message.

-   ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702199807451/ad87e735-339a-46f9-8f7a-f8b1bce092af.png?auto=compress,format&format=webp)

-   **POST /kaam:** Add a new task to the DynamoDB table.

-   ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702199884929/21223cd6-34d3-4288-aa4f-443aa2903ef6.png?auto=compress,format&format=webp)

    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702200112384/588ea903-2451-442f-b9e2-964f8925bb62.png?auto=compress,format&format=webp)

-   **GET /kaam:** Retrieve all tasks from the DynamoDB table.

    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702199928992/87e7f83b-7f78-407f-a1c8-a138fdaf7460.png?auto=compress,format&format=webp)

-   **PUT /kaam/{id}:** Update the completion status of a task in the DynamoDB table.

    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702199993916/4d3dec7b-f05e-4561-8ec2-68149637325f.png?auto=compress,format&format=webp)

    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702200234157/321b3bcd-7033-4738-84d3-95b7e33039ae.png?auto=compress,format&format=webp)

-   **POST /kaam/{id}:** Delete a task from the DynamoDB table.

    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702200046742/77ca8ebd-2572-4db5-aed2-3e1084aaeb80.png?auto=compress,format&format=webp)

    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702200265515/be2af028-9780-483e-876e-3e33408e3015.png?auto=compress,format&format=webp)

[](https://arjunmenon.hashnode.dev/building-a-serverless-nodejs-api-with-aws-and-serverless-framework#heading-conclusion "Permalink")
-------------------------------------------------------------------------------------------------------------------------------------

Conclusion
----------
