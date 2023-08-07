# Creating an S3 bucket

```text
S3 > Create bucket
Bucket name: employee-photo-bucket-<your initials>-<unique number>
```

# Modifying the S3 bucket policy

```text
S3 > Permissions > Bucket policy > Edit
```

```shell
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowS3ReadAccess",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::<INSERT-ACCOUNT-NUMBER>:role/S3DynamoDBFullAccessRole"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::<INSERT-BUCKET-NAME>",
                "arn:aws:s3:::<INSERT-BUCKET-NAME>/*"
            ]
        }
    ]
}
```