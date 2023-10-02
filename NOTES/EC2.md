# Amazon Elastic Compute Cloud

is a infrastructure as a service
Services:

- renting virtual machine (Elastic Cloud - EC2)
- storing data on virtual drives (Elastic Block Storage - EBS)
- distributer load accross machines (Elastic Load Balancer - ELB)
- scaling the service using auto scaling group (Auto Scaling Group - ASG)

## Sizing & Configuration Options

Operating System:

- Linux
- Windows
- MacOS

How much computing power (in cores) for CPU

How much random-access memory for RAM

How much storage space

- network attached (EBS & EFS)
- hardware (EC2)
- Network card
- Firewall Rules
- Bootstrap (to be configured at first launch)

## EC2 User Data

we can bootstrapping to do a one-time-script execution on the server

usually used for:

- installing updates
- installing software
- downloading common files from internet

the script runs on `sudo` (Root User)

## Instance Types

Naming convention for AWS' instance types
`<Instance Class> <Generation> . <Size within the class>`

example:
**m5.2xlarge**

| **attribute** | **explanation**                          |
| ------------- | ---------------------------------------- |
| m             | instance class                           |
| 5             | generation (AWS improves them over time) |
| 2xlarge       | size within the instance class           |

this is great for diverse type workloads
balance between:

- compute
- memory
- networking

### Compute Intensive

Ideal for compute-intensive tasks that require high performance processors

such as:

- **batch** processing workloads
- media **transcoding**
- high perf **Web Servers**
- high perf **computing** (HPC)
- scientific **modeling** & **Machine Learning**
- dedicated **Gaming Servers**

> Has prefix of C

### Memory Optimized

Ideal for workloads that process large data sets in memory (RAM)

such as:

- high **performance Databases**
- **Distributed** web scale **cache stores**
- **in-memory databases**, for BI (Business Inteligence)
- application performing **real-time of big unstructured data** (i.e. ElasticSearch)

> Has prefix of: R, X, High Memory, & z

### Storage Optimized

Ideal for storage instensive tasks, that require high, sequential read & write access to large data sets on local storage

such as:

- **high frequency** OLTP (Online Transactional Processing)
- Relational & NoSQL **databases**
- Cache for in-memory **databases**
- **Data Warehousing** Application
- Distributed **Filesystems**

> Has prefix of: I3, D, H

---

## SSH

### Access

#### Local / Personal Computer
To access ssh in local, makesure the ssh apps is available in the OS

then create pem file from the instance
make sure the name doesnt contain any space

```
$ ssh -i <location-of-pem-file> ec2-user@<public-ip>
```

#### EC2 Instance Connect

directly using browser to ssh into the server

### Best Practices

PROHIBITION:
1. never ever use ```$ aws configure``` 
and enter the IDs & keys directly in the instance itself
this might leakage of secret information to other users, use IAM role instead

---
## Purchasing Options

### On-Demand
- Pay as you use
- Has the highest cost
- Linux or Windows billed per second, after the first minute
- No upfront cost
- No commitment

Recommended For:
**short term** and **un-interrupted** workloads
for application with **unpredictable behaviors**

### Reserved
- Up to *72% **discount** compared to On-Demand ```* disc might be different than actual```
- Reserve **specific instance attributes** (Instance type, Region, Tenancy, OS)
- Reservation period: 
  - 1 year [%]
  - 3 years [%%]
- Payment Option:
  - No Upfront [%]
  - Partial Upfront [%%]
  - All Upfront [%%%]
- Reserve instance scope: Regional or Zonal(AZ)
- can be bought and sold in Reserved Instance Marketplace

> Convertible Reserved Instance:
> - Can change the EC2 instance type, family, OS, scope, & tenancy
> - Only up to 66% Discount

Recommended For:
**steady-state usage** application (such as DB)

### Saving Plans
- Up to *72% **discount** compared to On-Demand 
  ```*disc might be different than actual```
- **Commit to usage** i.e. $10/hour for 1 or 3 years
- Any usages that **exceed beyond** the commited treshold, billed at On-Demand rate
- Only applicable for **specific list** of instances (not aplicable for all types)
- Flexible accross:
  - Instance Sizes (m5.xlarge, m5.2xlarge)
  - OS (Linux, Windows, etc)
  - Tenancy (Host, Dedicated, Default)

### Spot Instances
- Currently deprecated
- Up to *90% **discount** compared to On-Demand 
  ```*disc might be different than actual```
- spot-instance price is **fluctuative** (but somehow predictable, determinded by AWS' supply & demand)
- BUT **can lose** at any point of time, 
    if our control cost "max-price" is cheaper than current spot price

Recommended For:
**Failure-Resilient** workloads:
batch jobs, data analysis, image processing
flexible starting & ending time services

> NOT FOR **CRITICAL** jobs or services

### Dedicated Hosts
- A **physical server** with EC2 instance capacity, dedicated
- Allows us to address **compliance requirements**:
  - i.e. per-socket, per-core software licenses
- Purchasing Options:
  - **On-Demand** [pay per sec for active Dedicated Hosts]
  - **Reserved** [1 or 3 years commitment with: No, Partial, or All Upfront]
- Most **expensive**

Recommended For:
Software that have **complicated licensing model** (**BYOL** - Bring Your Own License)
Companies that have **strong regulatory or compliance** needs

> **EC2 Dedicated Instances (similar variant)**
> - instances run on hardware thats dedicated to you
> - May share hardware with other instances in same account
> - no control over instance placement (start/stop)


### Capacity Reservation
- Reserve on demand in a specific AZ
- always access EC2 capacity when need it
- no time commitment, no billing discount
- combine regional reserved instances + saving plans 
- will be charged at On-Demand rate, whether the instance is running or off

Recommended For:
System that has **uninterrupted workloads** 
but also needs to be in a **specific Availability Zone**