#  Launching an EC2 Instance

```text
EC2 > Launch instances
Name: employee-directory-app
Amazon Machine Image: Amazon Linux 2023
Instance type: t2.micro

Key pair (login) > Create a new key pair
Key pair name: app-key-pair
Create key pair

Network settings > Edit
Subnet:first subnet 
Auto-assign Public IP: Enable

Firewall (security groups)
Create security group: app-sg

Inbound security groups rules > Remove above the ssh rule.

Add security group rule
Type > HTTP
Source type > Anywhere

Advanced details 
IAM instance profile: S3DynamoDBFullAccessRole

User data: 
```

```bash
#!/bin/bash -ex
wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/FlaskApp.zip
unzip FlaskApp.zip
cd FlaskApp/
yum -y install python3-pip
pip install -r requirements.txt
yum -y install stress
export PHOTOS_BUCKET=${SUB_PHOTOS_BUCKET}
export AWS_DEFAULT_REGION=<INSERT REGION HERE>
export DYNAMO_MODE=on
FLASK_APP=application.py /usr/local/bin/flask run --host=0.0.0.0 --port=80
```

```text
 Launch instance.
```

# Viewing the application

```bash
http://<Public IPv4 address>
```