Automate EC2 Start and Stop at Specific Times
Steps to Implement:
Create an IAM Role for Lambda

Go to IAM > Roles > Create Role
Select AWS Service → Lambda
Attach the policy:
AmazonEC2FullAccess (to start/stop instances)
Name the role (e.g., LambdaEC2StartStopRole)
Create a Lambda Function to Start EC2 Instances


Go to AWS Lambda → Create Function
Select Author from Scratch
Name: StartEC2Instances
Runtime: Python 3.9
Attach the IAM role (LambdaEC2StartStopRole)
Use the following code:


Create Another Lambda Function to Stop EC2 Instances
Name: StopEC2Instances
Use the following code:
Schedule Lambda with EventBridge (CloudWatch)



Go to Amazon EventBridge → Rules → Create Rule
Name: StartEC2InstancesRule
Select Schedule and set it to *cron(0 4 * * ? ) (10 AM UTC → Adjust for your timezone)
Target: Select Lambda function StartEC2Instances


Create another rule for stopping:
Name: StopEC2InstancesRule
Set cron to *cron(0 22 * * ? ) (10 PM UTC)
Target: Select Lambda function StopEC2Instances

