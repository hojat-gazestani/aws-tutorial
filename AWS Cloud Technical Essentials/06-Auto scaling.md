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