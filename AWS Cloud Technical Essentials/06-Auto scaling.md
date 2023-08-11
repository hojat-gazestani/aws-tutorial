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

# Creating the Auto Scaling group

```text
Auto Scaling > Auto Scaling Groups > Create Auto Scaling group > Choose launch template or configuration,
Auto Scaling group name: app-asg
Launch template: app-launch-template
Next

Choose instance launch options,
VPC: app-vpc
Availability Zones and subnets: Choose the Availability Zones with Public Subnet 1 and Public Subnet 2
Next

Configure advanced options
Load balancing: Attach to an existing load balancer
Attach to an existing load balancer: Choose from your load balancer target groups
Existing load balancer target groups: app-target-group
Health checks: ELB
Next

Configure group size and scaling policies
Desired capacity: 2
Minimum capacity: 2
Maximum capacity: 4
Scaling policies: Target tracking scaling policy
Target value: 60
Instances need: 300
Next

Add notifications > Add notification
SNS Topic: Create a topic
Send a notification to: app-sns-topic
With these recipients: Enter your email address
Next
Next
Create Auto Scaling group
```

# Testing the application
```shell
http://app-alb-123456789012.us-west-2.elb.amazonaws.com/info
```