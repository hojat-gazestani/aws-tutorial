# Setting up an IAM role for an EC2 instance

```text
IAM > Roles > Create role
Select trusted entity
Trusted entity type: AWS service
Use case: EC2
Next

permissions filter box: amazons3full > AmazonS3FullAccess
permissions filter box: amazondynamodb > AmazonDynamoDBFullAccess
Next

Role name: S3DynamoDBFullAccessRole
Create role
```