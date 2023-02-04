## What it is:
Provides scalable computing AWS resources 


## Features:
- Virtual computing environments known as *instances*.
- Preconfigured instance templates known as Amazon Machine Images (AMIs)
- Instance configurations known as *instance types*.
- Secure login information into your instance using *key-pair*.
- Volatile storage volumes - *instance store volume*.
- Persistent storage volumes - *Amazon Elastic Blocks (EBS)*
- Multiple physical locations for your resources known as *Regions* and *Availability Zones*.
- A firewall to control inbound and outbound traffic - *security group*.
- Static IPv4 addresses for dynamic computing known as *Elastic IP addresses*.
- Tags that can be assigned to EC2 resources. 
- Virtual networks that are logically isolated from the rest of the cloud known as *Virtual Private Clouds (VPC)*

## Pricing for AWS EC2 
EC2 services are charged per second with a minimum of 60s. Similarly, provisioned storage for EBS is also billed per second. 

- **Free tier**: free trial for selected AWS services that expire after 12 months from the date of service activation. The free tier offer is always available. For example, you can spin up a free-tier EC2 instance #1 that expires on December. A month later, you can spin up another free-tier EC2 instance #2 that expires on January. The expirations of independent services are independent.
- **On Demand** - No long-term commitments or upfront payment required. Recommended for: 
    - Low-costs and flexible usage without long-term commitment or upfront payment
    - Short-term, spiky applications with unpredictable workloads that cannot be interrupted.
    - Entry level 
- **Saving Plans** - reduce EC2 costs by making a commitment to a consistent amount of usage (in $/hr) for a term of 1 or 3 years (similar to a fixed-term pricing contract where you agree to pay at an agreeded upon rate for a fixed period of time). Users will be charged the Saving Plans rate for the fixed-term period. Two types of saving plans:
    - *Compute Savings* - most flexible, in which the plan is applied to EC2 instance usage regardless of type/family, AZ, etc. Allow users to change instance type, move between regions or move from EC2 to Fargate or Lambda at anytime. 
    - *Instance Savings* - lowest prices when commiting to a specific instance families in a Region. Allow users to change instance type, but restricted to instance family -i.e. c5.xlarge running Windows to c2.2xlarge running Linux. 
- **Reserved Instances** - reduce EC2 costs by making a commitment to a specific instance configuration, including instance type and region for a term of 1 or 3 years. Reserved Instances are charged monthly. Types of Reserved Instances: 
    - *Standard and Convertible Reserved Instances Pricing* - can change AZ, instance size, and networking type of their Standard Reserved Instances. Convertible Reserved Instances offers additional flexibility - i.e. different instance families, OS, or tenancies over Reserved Instance term. Convertible offers lower discount than Standard in general. 
    - *Payment Options* - no upfront - no upfront payment; users pay for discounted hourly rate, partial upfront - low upfront payment then discounted hourly rate, full upfront - pay for entire reserved term.  
- **Spot Instances** - request unused EC2 instances. Usage includes: 
    - Applications with flexible start and end times 
    - Feasible at very low prices
    - Urgent needs for a large amounts of additional capacity 

*Note*: AWS recommended Saving Plans over Reserved Instances due to flexibility. 

## Dedicated Hosts vs Dedicated Instances:
- **Dedicated Hosts** - allow users to use existing software licenses on EC2. Dedicated Hosts are physical server fully dedicated for a single user to address corporate compliance requirements. 
- **Dedicated Instances** - EC2 instances that run in a VPC on hardware that is dedicated to a single customer. Dedicated instances from different AWS accounts are physically isolated. However, dedicated instances may share hardware with other non-dedicated instances from the same AWS account. Can only be launched into an Amazon VPC. Note that if the VPC tenancy is ```default```, every instance launch into this VPC is ```default``` by nature unless other-wise specified. If the VPC tenancy is ```dedicated```, every instance launch into this VPC is ```dedicated```. 

*Note*: the primary difference between a dedicated host and a dedicated instance are that dedicated host has better control over how instances are placed on the host, allowing users to consistently deploy instances onto the same host overtime. 