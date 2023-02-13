# Infrastructure
## Region
AWS has Regions all around the world. A region is a cluster of data centres. 

## How to choose AWS Region
- Compliance - data and legal requirements 
- Proximity - reduce latency to users 
- Available Services - vary between regions 
- Pricing - vary between regions 

## Availability Zone:
- Each region has many availability zones (min = 3, max = 6). Each AZ is a discrete data centre with redundant power, networking, and connectivity. 
- They are separated so isolated from disaster. 
- The AZs are connected via high speed internet. 


## AWS Points of Presence (Edge Locations)
- Allow content to be delivered to users with low latency

## Some Global services: 
- IAM 
- Route53 (DNS)
- CloudFront (Content Delivery Network)
- WAF (Web application firewall)

# IAM - Global Service
## Users and Groups 
- Root account - default account created - shouldnt be used directly 
- Users - people within the organisations and can be grouped. 
- Groups only contain users and not other groups. 
- Users don't have to belong to a group, or can belong to multiple groups.

## Permissions
- Users and Groups can be assigned JSON documents called policies which define permissions. 
- Least privilege - don't give more permission than needed. 
- If a policy is applied to a group, all users in that group inherit that policy. 
- A policy can also be applied to individual users - inline policy.
- Consists of 
  - Version: version number (Always 2012-10-17)
  - Id: identifier for the policy 
  - Statement: one or more individual statements 
    - Sid - statement id 
    - Effect - Deny/Allow 
    - Principle - arn to which the policy is attached to 
    - Action - list of actions this policy allows or denies 
    - Resources - AWS resources 

## IAM Password Policy
- Stronger password  = better account security 
- Password Policy:
  - Min password Length
  - Special Characters
    - Lowercase, uppercase 
    - Numbers,
    - Non-alphanumeric
- Allow all IAM users to change password 
- Require changing password after some time (expiration)
- Prevent password resuse 

## IAM MFA 
- Password + MFA device
- Options:
  - Virtual MFA 
  - U2F Security Key - physical device
  - Hardware Key Fob 
  - Hardware Key Fob AWS CloudUS

## IAM Role
- AWS services assume IAM role to perform actions on users' behalf
- Entities that can get roles include 
  - AWS Services 
  - AWS account - entities in a different account 
  - Web Identity - users federated by specific external web identity provider to assume roles

## IAM Security Tools
- IAM Credentials Report (Account level) - report that lists all your account users and status of their credentials 
- IAM Access Advisor (User level) show the service permissions granted to a user and when those services were last accessed. Used to revise policies 


# EC2
## Main Features
- Rent Virtual Machine (EC2)
- Store data on virtual drives (EBS)
- Distribute loads across machines (ELB)
- Scale services auto scaling group (ASG)

## EC2 configurations
- OS
- CPU 
- RAM 
- Storage (EBS, EFS, drives)
- Network card - IP address
- Security Group
- Bootstrap script - EC2 User Data - run exactly once when an instance is first created - is a bash script 

## EC2 Instance types
- General Purpose - balance of compute, memory, networking - for applications that use resources in equal proportions as web servers and code repositories.
- Compute Optimised - (CPU Speed) applications that require high performance processors. Batch processing workloads, media transcoding, high performance webservers, HPC, etc
- Memory Optimised - (RAM) - for applications that require large dataset in memory. Relational/Nonrelational databases, web scale cache stores
- Accelerated Computing - hardware accelerators
- Storage Optimised - (SSD) require high sequential read write access to very large data set on local storage. OLTP, relational/non relational database, datawarehouse 

## Security Group 
- EC2 firewall that controls inbound and outbound traffic. 
- Contains only allow rules 
- Can be referenced by IP or by security group - i.e. allow traffic from another instance from an allowed security group
- What it controls: 
  - Port 
  - IP ranges IPv4, IPv6
  - Control of inbounds
  - Control of outbounds
- Can be attached to multiple instances 
- Locked down to a region/VPC combination
- Live outside EC2 - if traffic is blocked, EC2 instance won't see it
- All inbound traffics are blocked by default
- All outbound traffics are allowed by default 

## EC2 Pricing Options 
- On-Demand: pay for what you use - billed per second. Highest cost, no upfront. For short-term uninterrupted workloads
- Reserved instance:
  - Reserve an instance attribute (Type, Region, Tenancy, OS)
  - Period - 1 and 3 years 
  - Payment - No upfront, Partial, Full Upfront
  - Scope: Regional or Zonal
  - For steady-usage applications like a database.
- Convertible Reserved Instance: 
  - Similar to reserved instance, except can change instance type, family, OS, scope and tenancy
  - Lower discount 
- Saving Plan:
  - Discount based on long term usage
  - Commit to a certain rate of usage - i.e. ($10/hr for 1 or 3 years)
  - Locked to a specific family
  - Flexible across different attributes (type, os, scope, etc)
- Spot: 
  - Lose at any point if max price is less than spot price 
  - Useful for workload resilient to failures
    - Flexible start and end time 
    - Distributed workloads 
    - Not suitable for critical jobs or DBs
- Dedicated Host
  - Reserve a full physical server for compliance requirement
  - Use existing server bound software liscences (per-socket, per-core, per-VM software liscences)
  - Most expensive 
  - For software with complicated licensing (BYOL)
  - Strong regulatory requirements 
- Dedicated Instance: 
  - Run on hardware reserved for you 
  - Maybe a reserved node in a physical server - may share hardware with other instances in same account 
  - No control over instance placement 
- EC2 Capacity Reservation
  - Reserve on-demand instances capacity in a specific AZ for any duration
  - Access to EC2 capacity when needed 
  - No time commitment
  - Combine by Regional Reserved Instances and Saving Plans to benefit from billing discount
  - Charge whether the instance is running or not 
  - Suitable for short-term uninterrupted workloads that need to be in a specific AZ

## EC2 Spot instances and Spot Fleets
- Spot Fleets = set of Spot Instances + On-Demand Instances 
  - Try to meet target capacity with price constraints 
  - Launch pools (instance type, OS, AZ)
  - Strategies to allocate spot instances: 
    - Lowest Prices - from pool with lowest price 
    - Diversified - distributed across all pools
    - Capacity Optimised: optimal capacity for the number of instances 
- Request spot instances with lowest price