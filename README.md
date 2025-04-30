# EC2 AutoScaling with AWS CloudWatch using AWS CloudFormation with Nested Stacks

This project demonstrates how to implement automatic scaling of Amazon EC2 instances using AWS CloudWatch alarms and AWS CloudFormation templates. It employs a modular approach by utilizing nested stacks, where a parent stack orchestrates the creation of multiple child stacks.

## Overview

The infrastructure setup includes:

- **Amazon VPC**: A virtual private cloud to host the resources.
- **Amazon RDS**: A relational database service instance for persistent storage.
- **Amazon EC2 Auto Scaling Group**: A group of EC2 instances that can scale in or out based on demand.
- **Amazon CloudWatch Alarms**: Monitoring tools to trigger scaling actions based on CPU utilization.
- **Nested CloudFormation Stacks**: A parent stack that includes separate child stacks for VPC, RDS, and Auto Scaling configurations.

The use of nested stacks promotes reusability and better organization of CloudFormation templates.  ([How to sync cloudformation with github with nested stack?](https://stackoverflow.com/questions/79350106/how-to-sync-cloudformation-with-github-with-nested-stack?utm_source=chatgpt.com))

## Repository Structure

The repository contains the following YAML templates: ([aws-samples/ecs-refarch-cloudformation - GitHub](https://github.com/aws-samples/ecs-refarch-cloudformation?utm_source=chatgpt.com))

- `vpc-network.yaml`: Defines the VPC, subnets, and related networking components.
- `rds-database.yaml`: Sets up the RDS instance, including database configurations.
- `autoscaling.yaml`: Configures the Auto Scaling Group, launch configurations, and CloudWatch alarms.
- `wordpress-root.yaml`: The parent stack that references the above templates as nested stacks. ([Embed stacks within other stacks using nested stacks](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html?utm_source=chatgpt.com), [AWS::AutoScaling::AutoScalingGroup - AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-autoscaling-autoscalinggroup.html?utm_source=chatgpt.com))

## Deployment Instructions

1. **Upload Templates to S3**: Before deployment, upload all YAML templates to an Amazon S3 bucket. CloudFormation requires templates to be accessible via S3 URLs when using nested stacks.  ([How to sync cloudformation with github with nested stack?](https://stackoverflow.com/questions/79350106/how-to-sync-cloudformation-with-github-with-nested-stack?utm_source=chatgpt.com))

2. **Deploy Parent Stack**:
   - Navigate to the AWS CloudFormation console.
   - Choose "Create stack" and select "With new resources (standard)".
   - Provide the S3 URL for `wordpress-root.yaml`.
   - Follow the prompts to specify stack details and parameters.
   - Review and create the stack. ([Embed stacks within other stacks using nested stacks](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html?utm_source=chatgpt.com))

3. **Stack Management**:
   - The parent stack manages the lifecycle of all child stacks. Deleting the parent stack will automatically delete all associated child stacks.  ([Embed stacks within other stacks using nested stacks](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html?utm_source=chatgpt.com))

## Auto Scaling Configuration

The Auto Scaling Group is configured to:

- **Scale Out**: Add EC2 instances when CPU utilization exceeds a defined threshold.
- **Scale In**: Remove EC2 instances when CPU utilization falls below a defined threshold.

These scaling actions are triggered by CloudWatch alarms monitoring the average CPU utilization of the instances in the Auto Scaling Group.  ([Auto scaling CloudFormation template snippets - AWS Documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/quickref-autoscaling.html?utm_source=chatgpt.com))

## Prerequisites

- An active AWS account with permissions to create the following resources: VPC, EC2, RDS, Auto Scaling Groups, and CloudWatch alarms.
- AWS CLI configured with appropriate credentials.
- YAML templates uploaded to an S3 bucket accessible by CloudFormation. ([aws-samples/ecs-refarch-cloudformation - GitHub](https://github.com/aws-samples/ecs-refarch-cloudformation?utm_source=chatgpt.com), [How to sync cloudformation with github with nested stack?](https://stackoverflow.com/questions/79350106/how-to-sync-cloudformation-with-github-with-nested-stack?utm_source=chatgpt.com))

## License

This project is open-source and available under the [MIT License](LICENSE).

---

For more information and best practices on using nested stacks in AWS CloudFormation, refer to the [official AWS documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html). ([Embed stacks within other stacks using nested stacks](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html?utm_source=chatgpt.com))

--- 
