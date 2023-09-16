# AWS-Cloud-Cost-Optimization

# AWS DevOps Project: EBS Volume Cleanup

## Introduction

This project automates the process of identifying and cleaning up stale EBS (Elastic Block Store) volumes in your AWS environment. It uses AWS Lambda, SNS (Simple Notification Service), EC2 (Elastic Compute Cloud), and the Python boto3 library to achieve this.

### Project Goals

1. **Identify Unattached EBS Volumes**: The Lambda function will periodically search for EBS volumes that are not attached to any EC2 instances.

2. **Send Notifications**: When unattached EBS volumes are found, a notification is sent using SNS to notify the user or relevant stakeholders.

3. **Auto Deletion**: After 3 days of no action from the user, the Lambda function automatically deletes the stale EBS volumes to optimize costs and resources.

## Setup

### Prerequisites

- AWS Account: You need an AWS account with the necessary permissions to create Lambda functions, SNS topics, and perform EC2 and EBS operations.

- Python and Boto3: You must have Python installed on your local machine and install the Boto3 library.

### Configuration

1. **AWS Credentials**: Ensure that you have configured AWS credentials with appropriate permissions. You can do this by setting up AWS CLI or configuring the credentials in your Lambda function.

2. **Lambda Function**: Create a Lambda function using the provided Python script (lambda_function.py). Set up an appropriate schedule for the function to run periodically.

3. **SNS Topic**: Create an SNS topic for notifications and subscribe the desired email addresses or endpoints to it.

4. **IAM Permissions**: Ensure that the Lambda function's IAM role has permissions to list EC2 instances and volumes, send SNS messages, and delete EBS volumes. The policy should look like this:

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ec2:DescribeInstances",
                    "ec2:DescribeVolumes",
                    "ec2:DescribeVolumeStatus",
                    "ec2:DeleteVolume",
                    "sns:Publish"
                ],
                "Resource": "*"
            }
        ]
    }
    ```

5. **Environment Variables**: You may need to set environment variables within the Lambda function to specify the SNS topic ARN and the age limit (3 days).

6. **Testing**: Test the Lambda function manually to ensure it correctly identifies and sends notifications for unattached EBS volumes.

## Usage

1. The Lambda function will run according to its schedule and identify unattached EBS volumes.

2. When unattached volumes are found, it will send a notification to the specified SNS topic.

3. Users or stakeholders should receive notifications and take action within 3 days if needed.

4. If no action is taken within 3 days, the Lambda function will automatically delete the unattached EBS volumes.

## Maintenance

- Monitor SNS notifications and take necessary actions based on received alerts.

- Periodically review and update the Lambda function's schedule or configuration as needed.

## Contributing

Feel free to contribute to this project by opening issues, suggesting improvements, or creating pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- AWS for providing the cloud infrastructure and services necessary for this project.

- The open-source community for their contributions to the AWS Python SDK (Boto3).

---

Feel free to customize this README.md file to suit your project's specific details and requirements. Don't forget to include a license file (e.g., LICENSE) if needed.
