### AWS Lambda cron jobs
Sometimes, you'd need execute a certain lambda function periodically so that it can execute the required business logic.
With Serverless application model (SAM) this has been made incredibly easy to configure with `CloudWatchEvent` config.


Here is an example:

```yaml

  CronJob:
    Type: AWS::Serverless::Function
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

Schedule expressions are documented here: https://docs.aws.amazon.com/lambda/latest/dg/services-cloudwatchevents-expressions.html
