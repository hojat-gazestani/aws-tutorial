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

