# Amazon S3 Storage Classes
Amazon S3 offers a range of storage classes that you can choose from based on the data access, resiliency, and cost requirements of your workloads. S3 storage classes are purpose-built to provide the lowest cost storage for different access patterns. S3 storage classes are ideal for virtually any use case, including those with demanding performance needs, data residency requirements, unknown or changing access patterns, or archival storage. ***Not really important u can skip this..**
![Alt text](/Photos/Performance%20across%20the%20S3%20Storage%20Classes.png)
## General purpose - 
### S3 Standard
1. *High Availability and Durability*
    Data is stored redundantly across multiple devices in multiple facilities (>=3 AZs):
    - `99.99% availability`
    - `99.999999999% durability` (11 9's)
2. Perfect for frequently accessed data.
3. Suitable for Most Workloads : 
    - The default storage class.
    - Use cases include websites, content distribution, mobile and gaming applications, and big data analytics.
## Infrequent access - 
### S3 Standard-Infrequent Access (S3 Standard-IA)
*DESIGNED FOR INFREQUENTLY ACCESSED DATA*
1. Rapid Access : 
    Used for data that is accessed less frequently but requires rapid access when needed.
2. You Pay to Access the Data : 
    There is a low per-GB storage price and a per-GB retrieval fee.
3. Use Cases : 
    Great for long-term storage, backups, and as a data store for disaster recovery files.
### S3 One Zone Infrequent Access
Like S3 Standard-IA, but data is stored redundantly within a single AZ.
- Costs 20% less than regular S3 Standard-IA
- Great for long-lived, infrequently accessed, non-critical data.

`99.5% Availability
99.999999999% (11 9's) Durability`
## Unknown or changing access - 
### Amazon S3 Intelligent-Tiering
Amazon S3 Intelligent-Tiering is the first cloud storage that automatically reduces your storage costs on a granular object level by automatically moving data to the most cost-effective access tier based on access frequency, without performance impact, retrieval fees, or operational overhead.
- Optimizes Cost
- Monthly fee of $0.0025 per 1,000 objects

`99.99% Availability & 99.999999999% (11 9's) Durability`
![Alt text](/Photos/Highest%20cost.png)
## Archive - 
The Amazon S3 Glacier storage classes are purpose-built for data archiving, and are designed to provide you with the highest performance, the most retrieval flexibility, and the lowest cost archive storage in the cloud.
- You pay each time you access your data.
- Use only for archiving data.
- Glacier is cheap storage.
- Optimized for data that is very infrequently accessed.
### Amazon Glacier Instant Retrieval
Amazon S3 Glacier Instant Retrieval is an archive storage class that delivers the lowest-cost storage for long-lived data that is rarely accessed and requires retrieval in milliseconds.
### Amazon S3 Glacier Flexible Retrieval
S3 Glacier Flexible Retrieval delivers low-cost storage, up to 10% lower cost (than S3 Glacier Instant Retrieval), for archive data that is accessed 1—2 times per year and is retrieved asynchronously. For archive data that does not require immediate access but needs the flexibility to retrieve large sets of data at no cost, such as backup or disaster recovery use cases.
### Amazon S3 Glacier Deep Archive
S3 Glacier Deep Archive is Amazon S3’s lowest-cost storage class and supports long-term retention and digital preservation for data that may be accessed once or twice in a year. It is designed for customers—particularly those in highly-regulated industries, such as financial services, healthcare, and public sectors—that retain data sets for 7—10 years or longer to meet regulatory compliance requirements. S3 Glacier Deep Archive can also be used for backup and disaster recovery use cases, and is a cost-effective and easy-to-manage alternative to magnetic tape systems.
![Alt text](/Photos/Highest%20cost-1.png)