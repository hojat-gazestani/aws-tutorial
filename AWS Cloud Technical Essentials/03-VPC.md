# Creating the VPC

```text
VPC > Create VPC
Name tag: app-vpc
IPv4 CIDR block: 10.1.0.0/16

Create VPC
```

```text
Virtual private cloud > Internet gateways > Create internet gateway.
Name tag: app-igw
Create internet gateway.

details page > Actions > Attach to VPC
Available VPCs: app-vpc
Attach internet gateway
```

# Creating subnets
```text
Subnets > Create subnet
VPC ID: app-vpc

Subnet name:Public Subnet 1
Availability Zone: us-west-2a
IPv4 CIDR block: 10.1.1.0/24

Subnet name: Public Subnet 2
Availability Zone: us-west-2b
IPv4 CIDR block: 10.1.2.0/24

Subnet name: Private Subnet 1
Availability Zone: us-west-2a
IPv4 CIDR block: 10.1.3.0/24

Subnet name: Private Subnet 2
Availability Zone: us-west-2b
IPv4 CIDR block: 10.1.4.0/24
Create subnet.
```

```text
Public Subnet 1 > Actions > Edit subnet settings
Auto-assign IP settings: Enable auto-assign public IPv4 address
Save

Public Subnet 2 > Actions > Edit subnet settings
Auto-assign IP settings: Enable auto-assign public IPv4 address
Save
```

# Creating route tables

```text
VPC > Route Tables > Create route table
Name: app-routetable-public
VPC: app-vpc
Create route table
```

```text
route table details > app-routetable-public > Routes > Edit routes
Add route
Destination: 0.0.0.0/0
Target: Internet Gateway,app-igw
Save changes

Subnet associations >  Subnets without explicit associations  > Edit subnet associations
Select:
    Public Subnet 1
    Public Subnet 2

Save associations
```

```text
Route Tables > Create route table
Name: app-routetable-private
VPC: app-vpc
Create route table

app-routetable-private > Subnet associations > Subnets without explicit associations > Edit subnet associations.
Select:
    Private Subnet 1
    Private Subnet 2
Save associations
```