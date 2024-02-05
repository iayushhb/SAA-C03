# Deploying vCenter in AWS with VMware Cloud on AWS

### Why Use VMware on AWS?
VMware is used by organizations around the world for private cloud deployments. Some organizations opt for a hybrid cloud strategy and would like to leverage AWS services.

### Use Cases for VMware - 
- Hybrid Cloud : 
Connect your on-premises cloud to the AWS public cloud, and manage a hybrid workload.

- Cloud Migration : 
Migrate your existing cloud environment to AWS using
VMware's built-in tools.

- Disaster Recovery : 
VMware is famous for its disaster recovery technology. Using hybrid cloud, you can have an inexpensive disaster recovery environment on AWS.

- Leverage AWS : 
Use over 200 AWS services to update your applications or to create new ones.

### VMware Cloud on AWS
How is it deployed?

- It runs on dedicated hardware hosted in AWS using a single AWS account.
- Each host has two sockets with 18 cores per socket, 512 GiB RAM, and 15.2 TB Raw SSD storage.
- Each host is capable of running multiple VMware instances (up to the hundreds).
- Clusters can start with two hosts up to a maximum of 16 hosts per cluster.