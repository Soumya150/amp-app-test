# AWS IoT Core to Amazon SNS to Amazon SQS

This pattern contains a sample AWS CDK stack to create an IoT Rule with a SNS action, a SNS Topic and a SQS standard Queue subscribed to the SNS topic.

When a message is published to the IoT topic defined in the IoT Rule, this message will be published to the SNS topic and finally the message will be delivered to the SQS queue subscribed to the SNS topic

Learn more about this pattern at Serverless Land Patterns: https://serverlessland.com/patterns/iot-sns-sqs-cdk

Important: this application uses various AWS services and there are costs associated with these services after the Free Tier usage - please see the [AWS Pricing page](https://aws.amazon.com/pricing/) for details. You are responsible for any AWS costs incurred. No warranty is implied in this example.

## Requirements

* [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and log in. The IAM user that you use must have sufficient permissions to make necessary AWS service calls and manage AWS resources.
* [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) installed and configured
* [Git Installed](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node and NPM](https://nodejs.org/en/download/) installed
* [Python, pip, virtuenv](https://docs.aws.amazon.com/cdk/latest/guide/work-with-cdk-python.html) installed
* [AWS Cloud Development Kit](https://docs.aws.amazon.com/cdk/latest/guide/cli.html) (AWS CDK) installed

## Deployment Instructions

1. Clone the project to your local working directory

   ```sh
   git clone https://github.com/aws-samples/serverless-patterns/ 
   ```

2. Change the working directory to this pattern's directory

   ```sh
   cd serverless-patterns/iot-sns-sqs-cdk
   ```

3. Create and activate the project's virtual environment. This allows the project's dependencies to be installed locally in the project folder, instead of globally. Note that if you have multiple versions of Python installed, where the `python` command references Python 2.x, then you can reference Python 3.x by using the `python3` command. You can check which version of Python is being referenced by running the command `python --version` or `python3 --version`

   ```sh
    python -m venv .venv
    source .venv/bin/activate
   ```

4. Install the project dependencies

   ```sh
   python -m pip install -r requirements.txt
   ```

5. Deploy the stack to your default AWS account and region. 

   ```sh
   cdk deploy
   ```

## How it works

The CDK app deploys the resources and the IAM permissions required to run the application. 

## Testing

Log into the AWS Console, browse to AWS IoT Core:

1. In the AWS IoT Core Console, in the `Test` section (left-side pane), select the `MQTT test client`. 

2. Then under `Publish to a topic`, in the Topic filter field enter this: `device/data`, change the default Message payload to `{"default": "Hello from AWS IoT console"}`. Then click the `Publish` button.

3. In the AWS Console navigate to the SQS service. Select the SQS queue generated by the CDK stack (the name is in the format `iot-sns-sqs-cdk-IotSnsSqsCdkQueueXXXXXXX-XXXXX`)

4. In the `Receive messages` section, click on `Poll for messages`. This should display a new message. Click on the message ID and inspect the `Body` attributes which should contain the following:
```json
{
    ...
    "message": "Hello from AWS IoT console"
    ...
}
```

## Cleanup
 
Run the given command to delete the resources that were created. It might take some time for the CloudFormation stack to get deleted.

```sh
cdk destroy
```

----
Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved. 

SPDX-License-Identifier: MIT-0
