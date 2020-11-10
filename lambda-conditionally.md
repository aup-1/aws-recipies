### AWS Provision Resources Conditionally

Conditionals can be used when you want to provision certain resources based on the CloudFormation template input params.


In the following example this `CronJob` lambda only runs when `Env` is equal to `prod`.

```yaml
AWSTemplateFormatVersion: 2010-09-09
Transform: AWS::Serverless-2016-10-31
Description: Sample Template
    
Parameters:
  Env:
    Type: String    
Conditions:
   RunCronJob: !Equals [ !Ref Env, "prod" ]
CronJob:
    Type: AWS::Serverless::Function
    Condition: RunCronJob
    Properties:
      Role: !GetAtt CronJobRole.Arn
      Handler: renew-lambda.lambdaHandler
      Layers:
        - !Ref NodeDependenciesLayer
      CodeUri: /code/location
      FunctionName: 
      Runtime: nodejs12.x
      Events:
        CloudWatchEvent:
          Type: Schedule
          Properties:
            Schedule: rate(90 days)


```

Conditionals are documented here: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/conditions-section-structure.html
