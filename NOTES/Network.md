# Internet Protocol (IP)

## Public Network
Connection of Global Internet (World Wide Web)
- Public IP can be accessed throughout Internet
- Must unique accross the whole web
- can be geo-located

## Private Network
Connection of devices within specific scope
- Private IP only can be located in private network
- Different private networks COULD HAVE same private ip adress
- Need internet gateway (proxy) to connect to WWW

---
# Elastic IP 
Elastic IP is **a Public IPv4 IP we own** in AWS, until we delete it
    
    by default each time we stop and start an EC2 instance,
    its bound public IP might change

the Elastic IP can only bound for 1 instance or software
Default Elastic IP in one account (can ask AWS to increase the limit)

ElasticIP **charged after it has been allocated**, 
whether we **use it or not**

**Try to avoid using ElasticIP exclusively**
Why? *"They indicate poor architectural decision"*

> Recommendation:
> - Use random public IP and register DNS name on it
> - Use Load Balancer instead

---
# Placement Group
To strategize EC2 Instance placement

Several Strategise:
1. Cluster
    Cluster instances into a **low-latency group within a Single Availability Zone**
    ![PG Cluster](/images/pg-cluster.png)
2. Spread
    Spread instances across **DIFFERENT** hardwares (max 7 instances / group)
    recommended for Critical Applications, which need High Availability
3. Partition
    Separated from different partitions on different sets of rack
    recommended for High-Scale System such as Hadoop, Cassandra, Kafka

 

