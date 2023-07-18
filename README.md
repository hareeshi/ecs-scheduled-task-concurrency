# Run Amazon ECS Scheduled Tasks with Concurrency Limits

This solution addresses AWS Containers Roadmap issue 232 (https://github.com/aws/containers-roadmap/issues/232), which is to provide a way to define a concurrency limit for ECS scheduled tasks. While the ideal solution would be to introduce this as a native feature of Amazon ECS, this solution provides a workaround for achieving the desired outcome. 

This solution approach leverages a Step Functions state machine, which compares the number of running tasks to the requested concurrency limits, before running a new task. The state machine is triggered periodically (set to hourly in the reference CF) by an Amazon EventBridge rule.

The repository containers the CloudFormation template and State Machine Definition


# How to Deploy the Solution

1. Upload the State Machine Definition to an S3 bucket.
2. Edit the Cloudformation template to change the event schedule and concurrency limit, if needed.
3. Review the IAM policies defined in the CF template and see you can further lock it down to specific resources
4. Create a CloudFormation stack with the template. Provide relevant inputs, while creating the stack. 

# Todo
List of features to add
1. Add Concurrency Limit as a CF parameter
2. Add a configure wait and retry RunTask flow to the state machine
3. Tighten the IAM roles  

# Alternate Approaches

This solution focuses on how to achieve concurrency limits with ECS Scheduled Task feature. You can also achieve the same using AWS Batch, which is a fully managed service for running batch workloads. AWS Batch, behind the scenes, uses Amazon ECS for job orchestration.

