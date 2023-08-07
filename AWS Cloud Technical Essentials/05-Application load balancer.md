# Creating the Application Load Balancer

```text
EC2 > Load Balancing > Load Balancers > Create Load Balancer 
```

```text
Application Load Balancer > Create

Load balancer name: app-alb
Mappings: us-west-2a
First Availability Zone Subnet: Public Subnet 1
Second Availability Zone Subnet: Public Subnet 2
```

```text
Security groups > Create new security group
Security group name: load-balancer-sg
Description: HTTP access
VPC: app-vpc

Inbound rules: Add Rule
Type: HTTP
Source: Anywhere-IPv4
Create security group
```

```text
Listeners and routing > Create target group > Specify group details
Choose a target type: Keep Instances selected
Target group name: app-target-group
Health checks: Expand Advanced health check settings and configure the following:
Healthy threshold: 2
Unhealthy threshold: 5
Timeout:30
Interval: 40
Next
```

```text
Register targets: employee-directory-app-exercise7
Include as pending below

Create target group
```

```text
Create load balancer
 View load balancer
``` 

```text
Description > DNS name
http://app-elb-123456789012.us-west-2.elb.amazonaws.com
```

# Creating the launch template

```text
EC2 > Instances > Launch Templates > Create launch template
Launch template name: app-launch-template
Template version description: A web server for the employee directory application
Auto Scaling guidance: Provide guidance to help me set up a template that I can use with EC2 Auto Scaling
Application and OS Images (Amazon Machine Image) - required: Currently in use
Instance type: t2.micro
Key pair name: app-key-pair
Security groups: web-security-group

Advanced details
IAM instance profile: S3DynamoDBFullAccessRole

User data
```

```shell
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