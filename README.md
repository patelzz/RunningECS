# RunningECS
This is a CloudFormation template that uses ECS Tasks, Step Functions and CloudWatch Events alongside Simple Notification Service to run parallel tasks and send notifications if failures occur. Step Function logic is defined to specifically terminate long-running tasks and to re-try failed tasks before state machine termination.
