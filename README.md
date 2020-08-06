# AWS Tutorials

## [Jumpbox Architecture](jumpbox-architecture/)
From an Amazon EC2 instance in a private subnet of a VPC, try to communicate securely over the internet and  ping google.com


## [Static website on S3](static-page-s3)
Create an Amazon S3 bucket to host a static webpage that displays an image

## [Connect to RDS instance with Python](rds-connect)
Access to a MySQL RDS instance from Python, create a table and insert records 

## [Application Load Balancer w/Apache Web Server](alb-apache-web-server)
Host two identical web pages and provide their private or public IP, both pages should be hosted on two EC2's behing an Elastic Load Balancer



## Pre-requisites for most tutorials:

## Networking: VPC & Internet Gateway

### Step-1: VPC
Virtual Private cloud, is an isolated section of the AWS cloud where you can provision your infrastructure. 
**AWS Console** -> **Services** -> **VPC** -> **Your VPCs**
* Create VPC
* Choose **Name Tag**: Tutorials_VPC
* Specify a **IPv4 CIDR block**: 10.0.0.0/16
* Create

### Step-2: Internet Gateway
It is required for a subnet in order to be accessible to the internet since it allows internet traffict 
to and from your VPC.
Create an internet gateway and attach it to the VPC

**AWS Console** -> **Services** -> **VPC** -> **Internet Gateways**
* Create internet gateway
* Choose **Name Tag**: my-tutorials-internet-gateway
* Create

Choose the **internet gateway** -> **Actions** > **Attach to VPC** -> Select **Tutorials_VPC** -> **Attach internet gateway**


### Step-3: Public Subnet
Subnets are segments or partitions of a network divided by CIDR range.
**AWS Console** -> **Services** -> **VPC** -> Subnet
* Create subnet
* Choose **Name Tag**: Tutorial Public Subnet
* Choose the **VPC**: Tutorials_VPC
* Choose an **availability zone**: us-east-1a
* Specify an **IPv4 CIDR** block for the subnet from the range of your VPC: 10.0.1.0/24
* Create

### Step-4: Route table for public subnet
It specifies which external IP addresses are contactable from a subnet or internet gateway, in this case the private subnet is 
connected to the NAT Gateway and the public subnet is connected to the internet gateway.

**AWS Console** -> **Services** -> **VPC** ->Route Tables
* Create Route Table
* Choose **Name Tag**:  Tutorial RT for Public Subnet
* Choose the **VPC**: Tutorials_VPC
* Create

Go to the **Tutorial RT for Public Subnet** route table:
* Click on **Routes** tab -> **Edit routes**
* Click on **Add route** 
* Input 0.0.0.0/0 on the **destination** 
* On the **target** select **Internet Gateway** and the internet gateway my-tutorials-internet-gateway
* Save routes
        
* Go to the subnet, click on **Edit route table association** and select the **Tutorial RT for Public Subnet**


### Step-5: Private Subnet
**AWS Console** -> **Services** -> **VPC** -> **Subnet**
* Create subnet
* Choose **Name Tag**: Tutorial Private Subnet
* Choose the **VPC**: Tutorials_VPC
* Choose an **availability zone**: us-east-1a
* Specify an **IPv4 CIDR** block for the subnet from the range of your VPC: 10.0.2.0/24 (it should not overlap with the other subnet)
* Create

### Step-6: Route table for private subnet
**AWS Console** -> **Services** -> **VPC** -> **Route Tables**
* Create Route Table
* Choose **Name Tag**:  Tutorial RT for Private Subnet
* Choose the **VPC**: Tutorials_VPC
* Create


## Architecture
![Pre-requisites](pre-requisites.png)
        