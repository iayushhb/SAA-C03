# Theory for _AWS Certified Solutions Architect Associate (SAA-CO3)_

-   [`AWS Well-Architected Framework`](#aws-well-architected-framework)
-   [`IAM`](#identity-access-management)
-   [`S3`](#simple-storage-service)
-   [`EC2`](#elastic-compute-cloudec2)
-   [`EBS and EFS`](#elastic-block-storage-and-elastic-file-system)
-   [`DATABASES`](#databases)
-   [`VPC NETWORKING`](#virtual-private-cloud-vpc-networking)
-   [`ROUTE 53`](#route53)
-   [`ELASTIC LOAD BALANCERS`](#elastic-load-balancers-elb)
-   [`SCALING`](#scaling)
-   [`AUTO-SCALING`](#auto-scaling)
-   [`DECOUPLING WORKFLOWS`](#decoupling-workflows)
-   [`SIMPLE QUEUING SERVICE`](#simple-queuing-service-sqs)
-   [`SIMPLE NOTIFICATION SERVICE`](#simple-notification-service-sns)
-   [`API GATEWAY`](#api-gateway)
-   [`AWS BATCH`](#aws-batch)
-   [`AMAZON MQ`](#amazon-mq)
-   [`AWS STEP FUNCTIONS`](#aws-step-functions)
-   [`AMAZON APPFLOW`](#amazon-appflow)
- [`BIG DATA`](#big-data)


---

# AWS Well-Architected Framework

The AWS Well-Architected Framework helps you understand the pros and cons of decisions you
make while building systems on AWS. Using the Framework helps you learn architectural best
practices for designing and operating secure, reliable, efficient, cost-effective, and sustainable
workloads in the AWS Cloud. It provides a way for you to consistently measure your architectures
against best practices and identify areas for improvement.

### The pillars of the AWS Well-Architected Framework :

| Name                   | Description                                                                                                                                                                                                                                                                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Operational excellence | The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.                                                                                                                                         |
| Security               | The security pillar describes how to take advantage of cloud technologies to protect data, systems, and assets in a way that can improve your security posture.                                                                                                                                                                          |
| Reliability            | The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it’s expected to. This includes the ability to operate and test the workload through its total lifecycle. This paper provides in-depth, best practice guidance for implementing reliable workloads on AWS. |
| Performance efficiency | The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.                                                                                                                                                                               |
| Cost optimization      | The ability to run systems to deliver business value at the lowest price point.                                                                                                                                                                                                                                                          |
| Sustainability         | The ability to continually improve sustainability impacts by reducing energy consumption and increasing efficiency across all components of a workload by maximizing the benefits from the provisioned resources and minimizing the total resources required.                                                                            |

---

![alt text](/Photos/image.png)
![alt text](/Photos/image2.png)

---

# Identity Access Management

![alt text](/Photos/aws-iam.png)

### IAM allows you to manage users and their level of access to the AWS console.

_IAM offers a centralized hub of control within AWS and integrates with all other AWS Services._

-   Create users and grant permissions to those users.
-   Create groups and roles.
-   Control access to AWS resources.

## Root account :

The root account is the email address you used to sign up for AWS. The root account has full administrative access to AWS. **For this reason, it is important to secure this account**.

When you create the account you get two more generated items which are _access keys and secret access keys_ which are basically id and password for programatic access.

## 4 Steps to Secure Your AWS Root Account.

-   Enable multi-factor authentication on the root account.
-   Create an admin group for your administrators, and assign the appropriate permissions to this group.
-   Create user accounts for your administrators.
-   Add your users to the admin group.

## How do we control permissions ?

We assign permissions using policy documents , which are made of JSON(**JavaScript Object Notation**).

The documented rule sets that are applied to grant or limit access. In order for users, groups, or roles to properly set permissions, they use policies. Policies are written in JSON and you can either use custom policies for your specific needs or use the default policies set by AWS.

_Example of a Policy Document:_
![Alt text](/Photos/Json-eg.png)

\*_`IAM` is Universal_

\*_User has no permission when first created_

\*Access ID and secret keys aren’t the same as username and passwords. And only get to see them once , so save them in a secure location.

\*Always set up password rotations & you can create and customize your own rotation policies.

## The Building Blocks of IAM :

`User` : any individual end user such as an employee, system architect, CTO, etc.

`Groups` : any collection of similar people with shared permissions such as system administrators, HR employees, finance teams, etc. Each user within their specified group will inherit the permissions set for the group.

`Roles` : any software service that needs to be granted permissions to do its job, e.g- AWS Lambda needing write permissions to S3 or a fleet of EC2 instances needing read permissions from a RDS MySQL database.
It's similar to IAM user, however instead of being assiciated with one person , a role is intended to be assumed by anyone who needs it. Roles are temporary.

> It's best practice for users to _inherit permissions_ from groups. And that’s because if you didn’t then it would harder to manage people individually.

![Alt text](/Photos/policy-eg-iam.png)

> Always work on the principle that one user equals one physical person. Never share user accounts across multiple people.

## The principle of least privilege :

Only assign user the **minimum** amount of privileges they need to do their job.

### Example:

![Alt text](/Photos/iam-eg.png)

### Priority Levels in IAM:

Explicit Deny: Denies access to a particular resource and this ruling cannot be overruled.

Explicit Allow: Allows access to a particular resource so long as there is not an associated Explicit Deny.

Default Deny (or Implicit Deny): IAM identities start off with no resource access. Access instead must be granted.

### Identity providers and federation :

If you already manage user identities outside of AWS, you can use identity providers instead of creating IAM users in your AWS account. With an identity provider (IdP), you can manage your user identities outside of AWS and give these external user identities permissions to use AWS resources in your account. This is useful if your organization already has its own identity system, such as a corporate user directory. It is also useful if you are creating a mobile app or web application that requires access to AWS resources.

# Simple Storage Service

S3 stands for Simple Storage Service and it's a object storage in the cloud.

-   **Object Storage** : S3 provides secure, durable, highly scalable object storage.
-   **Scalable** : S3 allows you to store and retrieve any amount of data from anywhere on the web at a very low cost.
-   **Simple** : Amazon S3 is easy to use, with a simple web service interface.

![Alt text](/Photos/s3-logo.png)

#### S3 is object based storage -

Which means it manages data as objects rather than in file systems or data blocks.

> Example : You can store files like photos, videos, code, documents, text files etc.
> Basically you can store static files in S3. That means you can't store files like Database or Operating System.

## S3 basics

-   **Object type storage** : Store files in buckets (similar to folders).
-   **Can store large files** : Files can be from 0 bytes to 5 TB.
-   **Can't store dynamic files** : Not suitable to install an operating system or run a database on.
-   **Unlimited Storage** : The total volume of data and the number of objects you can store is unlimited.
-   The data consistency model for S3 ensures immediate read access for new objects after the initial PUT requests. These new objects are introduced into AWS for the first time and thus do not need to be updated anywhere so they are available immediately.

## Working with S3 Buckets

1. **Universal Namespace** : All AWS accounts share the S3 namespace. Each S3 bucket name is globally unique.
2. **Example S3 URLs** :

```
https://bucket-name.s3.region.amazonaws.com/key-name
https://acloudguru.s3.us-east-1.amazonaws.com/Ralphie.jpg
```

3. **Uploading Files** : When you upload a file to an S3 bucket, you will receive an HTTP 200 code if the upload was successful.

```
As S3 works on a key value principle -

- Key : The name of the object (e.g., Ralphie.jpg).

- Value : The data itself, which is made up of a sequence of bytes.

- Version ID : Important for storing multiple versions of the same object.

- Metadata : Data about the data you are storing (e.g., content-type, last-modified, etc).
```

### S3 is Highly available and highly durable

-   _Built for Availability_ : Built for 99.95% - 99.99% service availability, depending on the S3 tier.
-   _Designed for Durability_ : Designed for 99.999999999% (9 decimal places) durability for data stored in S3.

## Securing your data in S3

1. _Server-Side Encryption_ : You can set default encryption on a bucket to encrypt all new objects when they are stored in the bucket.
2. _Access Control Lists (ACLs)_ : Define which AWS accounts or groups are granted access and the type of access. You can attach S3 ACLs to individual objects within a bucket.
3. _Bucket Policies_ : S3 bucket policies specify what actions are allowed or denied (e.g., allow user Alice to PUT but not DELETE objects in the bucket).

### Securing your data with ACLs and Bucket Policies :

-   ACLs(Access Control Lists) : To secure object on an individual level.

    [![video](https://i9.ytimg.com/vi/XHWvg2DjwAY/mqdefault.jpg?sqp=CIS8ua4G-oaymwEmCMACELQB8quKqQMa8AEB-AH-CIAC0AWKAgwIABABGFUgQChyMA8=&rs=AOn4CLBMVAeOrbeE6MuA35hDz39CNNKjpg)](https://youtu.be/XHWvg2DjwAY)

-   Bucket Policies : To secure objects on an entire bucket level.

    [![Watch the video](https://i9.ytimg.com/vi/UW4y0gmOG5g/mqdefault.jpg?sqp=CKT0ua4G-oaymwEmCMACELQB8quKqQMa8AEB-AH-BYAC4AOKAgwIABABGFogXShlMA8=&rs=AOn4CLA0UVlgmevRn8UgnEchKCRyEPuXPg)](https://youtu.be/UW4y0gmOG5g)

## Versioning in S3 -

[![Watch the video](https://i9.ytimg.com/vi/_oO6xjMu0f8/mqdefault.jpg?sqp=CJDRua4G-oaymwEmCMACELQB8quKqQMa8AEB-AH-BYAC4AOKAgwIABABGEYgWShyMA8=&rs=AOn4CLCEFRAXklciJf80K7ZzfmT_sFZxgA)](https://youtu.be/_oO6xjMu0f8)

You can enable versioning in S3 so you can have multiple versions of an object within S3.

-   Contains all Versions : All versions of an object are stored in S3. This includes all writes and even if you delete an object.
-   Backup : Can be a great backup tool.
-   Cannot Be Disabled : Once enabled, versioning cannot be disabled — only suspended.
-   Lifecycle Rules : Can be integrated with lifecycle rules so you can set rules to expire or migrate data based on their version.
-   Supports MFA : Versioning also has MFA delete capability to provide an additional layer of security.

_If you enable versioning before creating your bucket then all objects will have a version id._

_If you upload new versions of objects then the bucket policy will only be applied on the new ones._

## Amazon S3 Storage Classes

Amazon S3 offers a range of storage classes that you can choose from based on the data access, resiliency, and cost requirements of your workloads. S3 storage classes are purpose-built to provide the lowest cost storage for different access patterns. S3 storage classes are ideal for virtually any use case, including those with demanding performance needs, data residency requirements, unknown or changing access patterns, or archival storage. **\*Not really important u can skip this..**
![Alt text](/Photos/Performance%20across%20the%20S3%20Storage%20Classes.png)

## General purpose -

### S3 Standard

1. _High Availability and Durability_
   Data is stored redundantly across multiple devices in multiple facilities (>=3 AZs):
    - `99.99% availability`
    - `99.999999999% durability` (11 9's)
2. Perfect for frequently accessed data.
3. Suitable for Most Workloads :
    - The default storage class.
    - Use cases include websites, content distribution, mobile and gaming applications, and big data analytics.

## Infrequent access -

### S3 Standard-Infrequent Access (S3 Standard-IA)

_DESIGNED FOR INFREQUENTLY ACCESSED DATA_

1. Rapid Access :
   Used for data that is accessed less frequently but requires rapid access when needed.
2. You Pay to Access the Data :
   There is a low per-GB storage price and a per-GB retrieval fee.
3. Use Cases :
   Great for long-term storage, backups, and as a data store for disaster recovery files.

### S3 One Zone Infrequent Access

Like S3 Standard-IA, but data is stored redundantly within a single AZ.

-   Costs 20% less than regular S3 Standard-IA
-   Great for long-lived, infrequently accessed, non-critical data.

`99.5% Availability
99.999999999% (11 9's) Durability`

## Unknown or changing access -

### Amazon S3 Intelligent-Tiering

Amazon S3 Intelligent-Tiering is the first cloud storage that automatically reduces your storage costs on a granular object level by automatically moving data to the most cost-effective access tier based on access frequency, without performance impact, retrieval fees, or operational overhead.

-   Optimizes Cost
-   Monthly fee of $0.0025 per 1,000 objects

`99.99% Availability & 99.999999999% (11 9's) Durability`
![Alt text](/Photos/Highest%20cost.png)

## Archive -

The Amazon S3 Glacier storage classes are purpose-built for data archiving, and are designed to provide you with the highest performance, the most retrieval flexibility, and the lowest cost archive storage in the cloud.

-   You pay each time you access your data.
-   Use only for archiving data.
-   Glacier is cheap storage.
-   Optimized for data that is very infrequently accessed.

### Amazon Glacier Instant Retrieval

Amazon S3 Glacier Instant Retrieval is an archive storage class that delivers the lowest-cost storage for long-lived data that is rarely accessed and requires retrieval in milliseconds.

### Amazon S3 Glacier Flexible Retrieval

S3 Glacier Flexible Retrieval delivers low-cost storage, up to 10% lower cost (than S3 Glacier Instant Retrieval), for archive data that is accessed 1—2 times per year and is retrieved asynchronously. For archive data that does not require immediate access but needs the flexibility to retrieve large sets of data at no cost, such as backup or disaster recovery use cases.

### Amazon S3 Glacier Deep Archive

S3 Glacier Deep Archive is Amazon S3’s lowest-cost storage class and supports long-term retention and digital preservation for data that may be accessed once or twice in a year. It is designed for customers—particularly those in highly-regulated industries, such as financial services, healthcare, and public sectors—that retain data sets for 7—10 years or longer to meet regulatory compliance requirements. S3 Glacier Deep Archive can also be used for backup and disaster recovery use cases, and is a cost-effective and easy-to-manage alternative to magnetic tape systems.
![Alt text](/Photos/Highest%20cost-1.png)

## Lifecycle Management with S3

-   Lifecycle Mangement automates moving your objects between different storage tiers, thereby maximizing cost effectiveness.
-   Can be used in conjunction with versioning.
-   Lifecycle rules can be applied to both current and previous versions of an object.

[![Watch the video](https://i9.ytimg.com/vi/bZ3sks1ruXg/mqdefault.jpg?sqp=CMDaua4G-oaymwEmCMACELQB8quKqQMa8AEB-AH-BYAC4AOKAgwIABABGGAgYChgMA8%3D&rs=AOn4CLBmmu48s2JS6B4N_k5VI5DCkaWXgg&retry=4)](https://youtu.be/bZ3sks1ruXg)

## S3 Object Lock

You can use S3 Object Lock to store objects using a write once, read many (WORM) model. It can help prevent objects from being deleted or modified for a fixed amount of time or indefinitely.

You can use S3 Object Lock to meet regulatory requirements that require WORM storage, or add an extra layer of protection against object changes and deletion.

## S3 Object Mode have 2 modes :

**Governance Mode** : In governance mode, users can't overwrite or delete an object version or alter its lock settings unless they have special permissions.

With governance mode, you protect objects against being deleted by most users, but you can still grant some users permission to alter the retention settings or delete the object if necessary.

**Compliance Mode** :
In compliance mode, a protected object version can't be overwritten or deleted by any user, including the root user in your AWS account. When an object is locked in compliance mode, its retention mode can't be changed and its retention period can't be shortened. Compliance mode ensures an object version can't be overwritten or deleted for the duration of the retention period.

### Retention Periods

A retention period protects an object version for a fixed amount of time. When you place a retention period on an object version, Amazon S3 stores a timestamp in the object version's metadata to indicate when the retention period expires.

After the retention period expires, the object version can be overwritten or deleted unless you also placed a legal hold on the object version.

### Legal Holds

S3 Object Lock also enables you to place a legal hold on an object version. Like a retention period, a legal hold prevents an object version from being overwritten or deleted. However, a legal hold doesn't have an associated retention period and remains in effect until removed.
Legal holds can be freely placed and removed by any user who has the s3 :PutObjectLegalHold permission.

## Glacier Vault Lock

S3 Glacier Vault Lock allows you to easily deploy and enforce compliance controls for individual
S3 Glacier vaults with a vault lock policy. You can specify controls, such as WORM, in a vault lock policy and lock the policy from future edits.
Once locked, the policy can no longer be changed.

## Encrypting S3 Objects -

### Types of Encryption :

1. **Encryption in Transit** :

    When the traffic passing between one endpoint to another is indecipherable. Anyone eavesdropping between server A and server B won’t be able to make sense of the information passing by. Encryption in transit for S3 is always achieved by SSL/TLS.

    - SSL/TLS
    - HTTPS

2. **Encryption at Rest**:

    When the immobile data sitting inside S3 is encrypted. If someone breaks into a server, they still won’t be able to access encrypted info within that server. Encryption at rest can be done either on the server-side or the client-side. The server-side is when S3 encrypts your data as it is being written to disk and decrypts it when you access it. The client-side is when you personally encrypt the object on your own and then upload it into S3 afterwards.

    ### Server-Side Encryption -

    _You encrypt files after uploading them to the cloud._

    **S3 Managed Keys / SSE - S3 (server side encryption S3 )**

    > When Amazon manages the encryption and decryption keys for you automatically. In this scenario, you concede a little control to Amazon in exchange for ease of use.

    **AWS Key Management Service / SSE - KMS**

    > When Amazon and you both manage the encryption and decryption keys together.

    **Server Side Encryption w/ customer provided keys / SSE - C**

    > When I give Amazon my own keys that I manage. In this scenario, you concede ease of use in exchange for more control.

    ### Client-Side Encryption -

    _You encrypt the files yourself before you upload them to S3._

> All Amazon S3 Buckets have encryption configured by default.
> All objects are automatically encrypted by using server-side encryption with Amazon S3 managed keys(SSE-S3).
> Applies to all objects in your S3 bucket.

Every time a file is uploaded to S3, a PUT request is initiated.
![Alt text](/Photos/put-request.png)

## Enforcing Server-Side Encryption using bucket policy

1. **x-amz-server-side-encryption**

    If the file is to be encrypted at the upload time, the `x-amz-server-side-encryption` parameter will be included in the request header.

2. You get 2 encryption types :

    `x-amz-server-side-encryption : AES256`
    (SSE-S3- - S3-Managed keys)

    `x-amz-server-side-encryption : aws:kms`
    (SSE-KMS -- KMS-Managed keys)

3. **PUT Request Header**

    When this parameter is included in the header of the PUT request, it tell S3 to encrypt the object at the time of upload, using the specified encryption method.

![Alt text](/Photos/put-req.png)

> If you want to change the encryption type of any object then just go to the object in the bucket and scroll down and you'll see `Server-side encryption settings`.

## Optimizing S3 Performance

**Types of Prefixes :**

1. mybucketname/folder1/subfolder1/myfile.jpg > /folderl/subfolder
2. mybucketname/folder2/subfolder1/myfile.jpg > /folder2/subfolder1
3. mybucketname/folder3/myfile.jpg >/folder3
4. mybucketname/folder4/subfolder4/myfile.jpg > /folder4/subfolder4
    > S3 has extremely low latency. You can get the first byte out of S3 within 100-200 milliseconds.
    > You can also achieve a high number of requests: 3,500
    > PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second, per prefix.

-   You can get better performance by spreading your reads across different prefixes. For example, if you are using 2
    prefixes, you can achieve 11,000 requests per second.
-   If we used all 4 prefixes in the last example, you would achieve 22,000 requests per second.

### S3 LIMITATIONS WHEN USING KMS

-   If you are using SSE-KMS to encrypt your objects in S3, you must keep in mind the KMS limits.
-   When you upload a file, you will call GenerateDataKey in the KMS API.
-   When you download a file, you will call Decrypt in the KMS API.

### KMS Request Rates

-   Uploading/downloading will count toward the KMS quota.
-   Region-specific, however, it's either 5,500, 10,000, or 30,000 requests per second.
-   Currently, you cannot request a quota increase for KMS.

## S3 Performance: Uploads

**Multipart Uploads**

-   Recommended for files over 100 MB
-   Required for files over 5 GB
-   Parallelize uploads (increases efficiency)
    ![Alt text](/Photos/s3-performance.png)

## S3 Performance: Downloads

**S3 Byte-Range Fetches**

-   Parallelize downloads by specifying byte ranges.
-   If there's a failure in the download, it's only for a specific byte range.
    ![Alt text](/Photos/s3-performance-downloads.png)

## Backing up Data with S3 Replication

Replication enables automatic, asynchronous copying of objects across Amazon S3 buckets. Buckets that are configured for object replication can be owned by the same AWS account or by different accounts. You can replicate objects to a single destination bucket or to multiple destination buckets. The destination buckets can be in different AWS Regions or within the same Region as the source bucket.

1. You can replicate objects from one bucket to another,
   Versioning must be enabled on both the source and destination buckets.
2. Objects in an existing bucket are not replicated automatically,
   Once replication is turned on, all subsequent updated objects will be replicated automatically. _Upload objects after turning on the replication_
3. Delete markers are not replicated by default,
   Deleting individual versions or delete markers will not be replicated._If you delete an item in the source bucket then the object in the destination bucket will not be deleted_

    [![Watch the video](https://i9.ytimg.com/vi/I19dMeKkms8/mqdefault.jpg?sqp=CKT0ua4G-oaymwEmCMACELQB8quKqQMa8AEB-AH-CIAC0AWKAgwIABABGFcgQihyMA8=&rs=AOn4CLDmc4ORTB7eHOMUR0ZxRD1HpWjuZw)](https://youtu.be/I19dMeKkms8)

---

# Elastic Compute Cloud(EC2)

![Alt text](/Photos/ec2-logo.png)

Amazon Elastic Compute Cloud (Amazon EC2) provides on-demand, scalable computing capacity in the Amazon Web Services (AWS) Cloud. Using Amazon EC2 reduces hardware costs so you can develop and deploy applications faster. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage. You can add capacity (scale up) to handle compute-heavy tasks, such as monthly or yearly processes, or spikes in website traffic. When usage decreases, you can reduce capacity (scale down) again.
Its configuration at launch is a live copy of the Amazon Machine Image (AMI) that you specify when you launched the instance.

> Like a VM, only hosted in AWS instead of your own data center.

-   _Pay only for what you use_
-   _Select the capacity right now, grow and shrink when you need_

EC2 has an extremely reduced time frame for provisioning and booting new instances and EC2 ensures that you pay as you go, pay for what you use, pay less as you use more, and pay even less when you reserve capacity. When your EC2 instance is running, you are charged on CPU, memory, storage, and networking. When it is stopped, you are only charged for EBS storage.

## EC2 Pricing Options

### On Demand Instances -

1. Low cost and flexibility of Amazon EC2 withoud any upfront payment or long-term commitment.
2. Used for Application with short-term , spiky or unpredictable workloads that cannot be interrupted.
3. Used for Applications that are being developed or tested on Amazon EC2 for the first time.

### Reserved Instances -

1. Used for Applications with steady state or predictable usage.
2. Used for Applications that require reserved capacity.
3. You can make upfront payments to reduce the total computing costs even further.
4. With Standard-RIs you can upto save 72% off the on demand price.
5. With Convertable RIs you can save upto 54% off the on demand price. which have the option to change to a different RI type of equal or greater value.
6. With scheduled RI you can launch within the time window you define. Match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day , week or month.

\***_Reserved Instances Operate at regional level_**

#### Savings Plan with Reserved Instances -

1. Save up to 72% : All AWS compute usage, regardless of instance type or Region.
2. Commit to 1 or 3 Years : Commit to use a specific amount of compute power (measured by the hour) for a 1-year or 3-year period.
3. Super Flexible : Not only EC2, this also includes serverless.

#### Standard Reserved vs. Convertible Reserved vs. Scheduled Reserved:

-   Standard Reserved Instances have inflexible reservations that are discounted at 75% off of On-Demand instances. Standard Reserved Instances cannot be moved between regions. You can choose if a Reserved Instance applies to either a specific Availability Zone, or an Entire Region, but you cannot change the region.
-   Convertible Reserved Instances are instances that are discounted at 54% off of On-Demand instances, but you can also modify the instance type at any point. For example, you suspect that after a few months your VM might need to change from general purpose to memory optimized, but you aren't sure just yet. So if you think that in the future you might need to change your VM type or upgrade your VMs capacity, choose Convertible Reserved Instances. There is no downgrading instance type with this option though.
-   Scheduled Reserved Instances are reserved according to a specified timeline that you set. For example, you might use Scheduled Reserved Instances if you run education software that only needs to be available during school hours. This option allows you to better match your needed capacity with a recurring schedule so that you can save money.

## Spot Instances -

A Spot Instance is an instance that uses spare EC2 capacity that is available for less than the On-Demand price. Because Spot Instances enable you to request unused EC2 instances at steep discounts, you can lower your Amazon EC2 costs significantly. The hourly price for a Spot Instance is called a Spot price. The Spot price of each instance type in each Availability Zone is set by Amazon EC2, and is adjusted gradually based on the long-term supply of and demand for Spot Instances. Your Spot Instance runs whenever capacity is available.
![Alt text](/Photos/spot-req.png)
_To terminate your spot instances you need to first cancel the spot request and then terminate the instances._

**When to use spot instances :**
![Alt text](/Photos/ec2-spot.png)

-   Big data analysis.
-   Containerized workloads.
-   CI/CD testing.
-   Image and media rendering.
-   High performance computing.

**When not to use spot instances :**

-   Persistent workloads.
-   Critical jobs.
-   Databases.

### Spot Fleet :

A Spot Fleet is a set of Spot Instances and optionally On-Demand Instances that is launched based on criteria that you specify. The Spot Fleet selects the Spot capacity pools that meet your needs and launches Spot Instances to meet the target capacity for the fleet. By default, Spot Fleets are set to maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated. You can submit a Spot Fleet as a one-time request, which does not persist after the instances have been terminated. You can include On-Demand Instance requests in a Spot Fleet request.

#### You can have the following strategies with Spot Fleets :

-   _capacityOptimized_ :
    The Spot Instances come from the pool with optimal capacity for the number of instances launching.
-   _lowestPrice_ :
    The Spot Instances come from the pool with the lowest price. This is the default strategy.
-   _diversified_ :
    The Spot Instances are distributed across all pools.
-   _InstancePoolsToUseCount_ :
    The Spot Instances are distributed across the number of Spot Instance pools you specify. This parameter is valid only when used in combination with lowestPrice.

## Dedicated Hosts -

1. **Compliance** : Regulatory requirements that may not support multi-tenant virtualization.
2. **Licensing** : Great for licensing that does not support multi-tenancy or cloud deployments.
3. **On-Demand** : Can be purchased on-demand (hourly).
4. **Reserved** : Can be purchased as a reservation for up to 70% off the on-demand price.

**Dedicated Hosts allow you to use your existing per-socket, per-core, or per-VM software licenses. When you bring your own license, you are responsible for managing your own licenses. However, Amazon EC2 has features that help you maintain license compliance, such as instance affinity and targeted placement.**

| Instance state  | Description                                                                                                                                                                                 | Billing                                                           |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `pending`       | The instance is preparing to enter the `running` state. An instance enters the pending state when it launches for the first time, or when it is started after being in the `stopped` state. | Not billed                                                        |
| `running`       | The instance is running and ready for use.                                                                                                                                                  | Billed                                                            |
| `stopping`      | The instance is preparing to be stopped or stop-hibernated.                                                                                                                                 | Not billed if preparing to stop. Billed if preparing to hibernate |
| `stopped`       | The instance is shut down and cannot be used. The instance can be started at any time.                                                                                                      | Not billed                                                        |
| `shutting-down` | The instance is preparing to be terminated.                                                                                                                                                 | Not billed                                                        |
| `terminated`    | The instance has been permanently deleted and cannot be started.                                                                                                                            | Not billed                                                        |

## Roles in AWS

An IAM role is an IAM identity that you can create in your account that has specific permissions. An IAM role is similar to an IAM user, in that it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it. Also, a role does not have standard long-term credentials such as a password or access keys associated with it. Instead, when you assume a role, it provides you with temporary security credentials for your role session.

# Security Groups and Bootstrap Scripts

> Note -
>
> -   Linux : SSH - PORT 22
> -   Windows : RDP - PORT 3389
> -   HTTP : WEB BROWSING - PORT 80
> -   HTTPS : ENCRYPTED WEB BROWSING (SSL) - PORT 443

## Security Groups :

Security groups are virtual firewalls for your ec2 isntances . By default , everything is blocked.

**To let everything in : 0.0.0.0/0**

_In order to communicate with your ec2 instances via SSH/RDP/HTTP, you will need to open up the correct ports._

## Bootstrap scripts :

A script that runs when an instance first runs.

Ex :

```
#!/bin/bash
yum install httpd -y
#installs apache
yum service httpd start
#starts apache
```

_Adding these tasks at boot time adds to the amount of time it takes to boot the instance.
However, it allows you to automate the installation of applications._

## EC2 Metadata & Userdata

EC2 metadata is simply data about your EC2
instance.

This can include information such as private IP address, public IP
address, hostname, security groups, etc.

_Using the `curl` command we can query metadata about our ec2 instance._

And also, with a simple bootstrap(user data) script we can use the curl command to save our ec2 metadata.

## Implementation -

1. Create an ec2 instance and paste this bootstrap script. and add http ,https and ssh as security rules. and enable metadata and select what IDMS(Instance Metadata Service) version you wanna use.

**For IMDSv1**

_Use Amazon Linux 2 instance_

```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
cd /var/www/html
echo "<html><body><h1>My IP is" > index.html
curl http://169.254.169.254/latest/meta-data/public-ipv4 >> index.html
echo "</h1></body></html>" >> index.html
```

**For IMDSv2**

_Use Amazon Linux 2023 instance_

```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
cd /var/www/html
echo "<html><body><h1>My IP is" > index.html
TOKEN=$(curl -s -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
PUBLIC_IP=$(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/public-ipv4)
echo "$PUBLIC_IP" >> index.html
echo "</h1></body></html>" >> index.html
```

2. Now copy your public-ip4 ip and paste it in browser.
   ![Alt text](/Photos/metadata-page.png)

## Networking with EC2

**An ENI will be attached by default to the ec2 instance you create.**

### Security Groups

Security Groups are used to control access (SSH, HTTP, RDP, etc.) with EC2. They act as a virtual firewall for your instances to control inbound and outbound traffic. When you launch an instance in a VPC, you can assign up to five security groups to the instance and security groups act at the instance level, not the subnet level.

**Security Groups Key Details:**

-   Security groups control inbound and outbound traffic for your instances (they act as a Firewall for EC2 Instances) while NACLs control inbound and outbound traffic for your subnets (they act as a Firewall for Subnets). Security Groups usually control the list of ports that are allowed to be used by your EC2 instances and the NACLs control which network or list of IP addresses can connect to your whole VPC.
-   Every time you make a change to a security group, that change occurs immediately
-   Whenever you create an inbound rule, an outbound rule is created immediately. This is because Security Groups are stateful. This means that when you create an ingress rule for a security group, a corresponding egress rule is created to match it. This is in contrast with NACLs which are stateless and require manual intervention for creating both inbound and outbound rules.
-   Security Group rules are based on ALLOWs and there is no concept of DENY when in comes to Security Groups. This means you cannot explicitly deny or blacklist specific ports via Security Groups, you can only implicitly deny them by excluding them in your ALLOWs list
-   Because of the above detail, everything is blocked by default. You must go in and intentionally allow access for certain ports.
-   Security groups are specific to a single VPC, so you can't share a Security Group between multiple VPCs. However, you can copy a Security Group to create a new Security Group with the same rules in another VPC for the same AWS Account.
-   Security Groups are regional and can span AZs, but can't be cross-regional.
-   Outbound rules exist if you need to connect your server to a different service such as an API endpoint or a DB backend. You need to enable the ALLOW rule for the correct port though so that traffic can leave EC2 and enter the other AWS service.
-   You can attach multiple security groups to one EC2 instance and you can have multiple EC2 instances under the umbrella of one security group
-   You can specify the source of your security group (basically who is allowed to bypass the virtual firewall) to be a single /32 IP address, an IP range, or even a separate security group.
-   You cannot block specific IP addresses with Security Groups (use NACLs instead)
-   You can increase your Security Group limit by submitting a request to AWS

You can attach 3 types of virtual networking cards to your EC2 instances.

### Elastic Network Interfaces

**ENI Simplified:** An elastic network interface is a networking component that represents a virtual network card. When you provision a new instance, there will be an ENI attached automatically and you can create and configure additional network interfaces if desired. When you move a network interface from one instance to another, network traffic is redirected to the new instance.

**ENI Key Details:**

-   ENI is used mainly for low-budget, high-availability network solutions.

-   However, if you suspect you need high network throughput then you can use Enhanced Networking ENI.

-   Adding more ENIs won’t necessarily speed up your network throughput, but Enhanced Networking ENI will.

-   You can attach a network interface to an EC2 instance in the following ways:
    -   When it's running (hot attach)
    -   When it's stopped (warm attach)
    -   When the instance is being launched (cold attach).
-   If an EC2 instance fails with ENI properly configured, you (or more likely,the code running on your behalf) can attach the network interface to a hot standby instance. Because ENI interfaces maintain their own private IP addresses, Elastic IP addresses, and MAC address, network traffic will begin to flow to the standby instance as soon as you attach the network interface on the replacement instance. Users will experience a brief loss of connectivity between the time the instance fails and the time that the network interface is attached to the standby instance, but no changes to the VPC route table or your DNS server are required.

-   You can enable a VPC flow log on your network interface to capture information about the IP traffic going to and from a network interface.

An elastic network interface is a logical networking component in a VPC that represents a virtual network card. It can include the following attributes:

-   A primary private IPv4 address from the IPv4 address range of your VPC
-   A primary IPv6 address from the IPv6 address range of your VPC
-   One or more secondary private IPv4 addresses from the IPv4 address range of your VPC
-   One Elastic IP address (IPv4) per private IPv4 address
-   One public IPv4 address
-   One or more IPv6 addresses
-   One or more security groups
-   A MAC address
-   A source/destination check flag

_The default ENI of an EC2 instance :_

![Alt text](/Photos/eni-ec2.png)

## Enhanced Networking on Linux

**For high performance networking between 10Gbps - 100Gbps**

Enhanced networking uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on supported instance types. SR-IOV is a method of device virtualization that provides higher I/O performance and lower CPU utilization when compared to traditional virtualized network interfaces. Enhanced networking provides higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies. There is no additional charge for using enhanced networking.

_Contents_ -

-   Enhanced networking support
-   Enable enhanced networking on your instance
-   Elastic Network Adapter (ENA)
-   ENA Express
-   Intel 82599 VF
-   Operating system optimizations
-   Network performance metrics
-   Troubleshoot ENA
-   Improve network latency on Linux instances

#### Enhanced Networking support :

All current generation instance types support enhanced networking, except for T2 instances.

**You can enable enhanced networking using one of the following mechanisms:**

1. Elastic Network Adapter (ENA) :
   The Elastic Network Adapter (ENA) supports network speeds of up to 100 Gbps for supported instance types.

2. Intel 82599 Virtual Function (VF) interface :
   The Intel 82599 Virtual Function interface supports network speeds of up to 10 Gbps for supported instance types. Typically used on older instances.

## Elastic Fabric Adapter

An Elastic Fabric Adapter (EFA) is a network device that you can attach to your Amazon EC2 instance to accelerate High Performance Computing (HPC) and machine learning applications. EFA enables you to achieve the application performance of an on-premises HPC cluster, with the scalability, flexibility, and elasticity provided by the AWS Cloud.

EFAs provide lower and more consistent latency and higher throughput than the TCP transport traditionally used in cloud-based HPC systems. It enhances the performance of inter-instance communication that is critical for scaling HPC and machine learning applications. It is optimized to work on the existing AWS network infrastructure and it can scale depending on application requirements.

**Differences between EFAs and ENAs -**

Elastic Network Adapters (ENAs) provide traditional IP networking features that are required to support VPC networking. EFAs provide all of the same traditional IP networking features as ENAs, and they also support OS-bypass capabilities. OS-bypass enables HPC and machine learning applications to bypass the operating system kernel and to communicate directly with the EFA device.

> _Note_ : By default, the public IP address of an EC2 Instance is released when the instance is stopped even if its stopped temporarily. Therefore, it is best to refer to an instance by its external DNS hostname. If you require a persistent public IP address that can be associated to the same instance, use an Elastic IP address which is basically a static IP address instead.

## Optimizing with EC2 Placement Groups

Placement groups balance the tradeoff between risk tolerance and network performance when it comes to your fleet of EC2 instances. The more you care about risk, the more isolated you want your instances to be from each other. The more you care about performance, the more conjoined you want your instances to be with each other.

1. Cluster – packs instances close together inside an Availability Zone. This strategy enables workloads to achieve the low-latency network performance necessary for tightly-coupled node-to-node communication that is typical of high-performance computing (HPC) applications.

    ![Alt text](/Photos/cluster-ec2.png)

2. Partition – spreads your instances across logical partitions such that groups of instances in one partition do not share the underlying hardware with groups of instances in different partitions. This strategy is typically used by large distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka.
   ![Alt text](/Photos/partition-ec2.png)

3. Spread – strictly places a small group of instances across distinct underlying hardware to reduce correlated failures.
   ![Alt text](/Photos/spread-ec2.png)

# Deploying vCenter in AWS with VMware Cloud on AWS

### Why Use VMware on AWS?

VMware is used by organizations around the world for private cloud deployments. Some organizations opt for a hybrid cloud strategy and would like to leverage AWS services.

### Use Cases for VMware -

-   Hybrid Cloud :
    Connect your on-premises cloud to the AWS public cloud, and manage a hybrid workload.

-   Cloud Migration :
    Migrate your existing cloud environment to AWS using
    VMware's built-in tools.

-   Disaster Recovery :
    VMware is famous for its disaster recovery technology. Using hybrid cloud, you can have an inexpensive disaster recovery environment on AWS.

-   Leverage AWS :
    Use over 200 AWS services to update your applications or to create new ones.

### VMware Cloud on AWS

How is it deployed?

-   It runs on dedicated hardware hosted in AWS using a single AWS account.
-   Each host has two sockets with 18 cores per socket, 512 GiB RAM, and 15.2 TB Raw SSD storage.
-   Each host is capable of running multiple VMware instances (up to the hundreds).
-   Clusters can start with two hosts up to a maximum of 16 hosts per cluster.

## Extending AWS Beyond the Cloud with AWS Outposts

## What Is Outposts?

Outposts brings the AWS data center directly to you, on-premises. Outposts allows you to have the large variety of AWS services in your data center. You can have Outposts in sizes such as 1U and 2U servers all the way up to 42U racks and multiple-rack deployments.

![Alt text](/Photos/outposts.png)

### Benefits of Outposts -

-   Hybrid Cloud :
    Create a hybrid cloud where you can leverage AWS services inside your own data center.
-   Consistency :
    Bring the AWS Management Console, APIs, and SDKs into your data center, allowing uniform consistency in your hybrid environment.
-   Fully Managed Infrastructure :
    AWS can manage the infrastructure for you. You do not need a dedicated team to look after your Outposts infrastructure.

### Outposts Family Members :

| Outposts Rack                                                                             | Outposts Servers                                                                                                                           |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| _Hardware_ : Available starting with a single 42U rack and scale up to 96 racks           | _Hardware_ : Individual servers in 1U or 2U form factor                                                                                    |
| _Services_ : Provides AWS compute, storage, database, and other services locally          | _Use Cases_ : Useful for small space requirements, such as retail stores, branch offices, healthcare provider locations, or factory floors |
| _Results_ : Gives the same AWS infrastructure, services, and APIs in your own data center | _Results_ : Provides local compute and networking services                                                                                 |

#### Process :

-   Order :
    Log in to the AWS Management Console, and order your Outposts configuration.
-   Install :
    AWS staff will come on-site to install and deploy the hardware, including power, networking, and connectivity.
-   Launch :
    Using the AWS Management Console, you can launch instances on your Outpost on-site.
-   Build :
    Start building your on-site AWS environment.

---

# Elastic Block Storage and Elastic File System

---

# EBS

An Amazon EBS volume is a durable, block-level storage device that you can attach to a single EC2 instance. You can think of EBS as a cloud-based virtual hard disk. You can use EBS volumes as primary storage for data that requires frequent updates, such as the system drive for an instance or storage for a database application. You can also use them for throughput-intensive applications that perform continuous disk scans.

![Alt text](/Photos/ebs-logo.png)

We reccommend Amazon EBS for data that must be quickly accessible and requires long-term persistence. EBS volumes are particularly well-suited for use as the primary storage for file systems, databases, or for any applications that require fine granular updates and access to raw, unformatted, block-level storage. Amazon EBS is well suited to both database-style applications that rely on random reads and writes, and to throughput-intensive applications that perform long, continuous reads and writes.

**EBS Usecase** :

-   Create a file system.
-   Run a database.
-   Run an operating system.
-   Store Data.
-   Install applications.

_With Amazon EBS, you pay only for what you use._

**Features** :

-   Designed for mission-critical workloads.
-   Dynamically increase capacity and change the volume type with no downtown or performance impact to your live systems.
-   Amazon EBS provides the ability to create snapshots (backups) of any EBS volume and write a copy of the data in the volume to S3, where it is stored redundantly in multiple Availability Zones

#### EBS Details :

-   Your EBS volumes will always be in the same AZ as the EC2 instance to which it is attached.
-   You can resize EBS volumes on the fly. You do not need to stop or restart the instance. However, you will need to extend the filesystem in the OS so the OS can see the resized volume.
-   You can change volume types on the fly (e.g., go from gp2 to io2). You do not need to stop or restart the instance.

### EBS Volume Types :

-   **SSD**(Solid State Disk) :

    -   _General Purpose SSD(gp2)_:
        _A balance of price and performance._

        1. 3 IOPS per GiB, upto a maximum of 16000 IOPS per volume.

        2. gp2 volumes smaller than 1 TB can burst upto 30000 IOPS.

        3. Good for boot volumes or development and test applications that are not latency sensitive.

    -   _General Purpose SSD(gp3)_:

        1. Predictable 3,000 IOPS baseline performance and 125 MiB/s regardless of volume size.
        2. Ideal for applications that require high performance at a low cost, such as MySQL, Cassandra, virtual desktops, and Hadoop analytics.
        3. Customers looking for higher performance can scale up to 16,000 IOPS and 1,000 MiB/s for an additional fee.
        4. The top performance of gp3 is 4 times faster than max throughput of gp2 volumes.

    -   _Provisioned IOPS SSD (io1)_:

        The high-performance option and the most expensive

        1. Up to 64,000 IOPS per volume. 50 1OPS per GiB.

        2. Use if you need more than 16,000 IOPS.

        3. Designed for I/O-intensive applications, large databases, and latency-sensitive workloads.

    -   _Provisioned IOPS SSD (io2)_:

        Latest generation. Higher durability and more IOPS, i02 is the same price as i01.

        1. 500 IOPS per GiB. Up to 64,000 IOPS.

        2. 99.999% durability instead of up to 999%.

        3. 1/0-intensive apps, large databases, and latency-sensitive workloads.Applications that need high levels of durability.

-   **HDD**(Hard Disk Drive) - MB/s Intensive:
    -   _Throughput Optimized HDD (st1)_:
        Low-cost HDD volume.
        1. Baseline throughput of 40 MB/s per TB
        2. Ability to burst up to 250 MB/s per TB
        3. Maximum throughput of 500 MB/s per volume
        4. Frequently accessed, throughput-intensive workloads
        5. Big data, data warehouses, ETL, and log processing
        6. A cost-effective way to store mountains of data
        7. Cannot be a boot volume
    -   _COLD HDD (SC1)_:
        Lowest Cost Option.
        1. Baseline throughput of 12 MB/s per TB
        2. Ability to burst up to 80 MB/s per TB
        3. Max throughput of 250 MB/s per volume
        4. A good choice for colder data requiring fewer scans per day
        5. Good for applications that need the lowest cost and performance is not a factor
        6. Cannot be a boot volume

![alt text](/Photos/iopsvsthru.jpeg)

### Volumes :

THINK OF VOLUME AS A VIRTUAL HARD DISK
Volumes are simply virtual hard disks. You need a minimum of 1 volume per EC2 instance. This is called the root device volume.

### Snapshot :

-   Think of snapshots as a photograph of the virtual disk/volume.
-   When you take a snapshot, it is a point-in-time copy of a volume.
-   This means only the data that has been changed since your last snapshot are moved to S3. This saves dramatically on space and the time it takes to take a snapshot.
-   If it is your first snapshot, it may take some time to create as there is no previous point-in-time copy.

#### Tips -

-   Snapshots only capture data that has been written to your Amazon EBS volume, which might exclude any data that has been locally cached by your application or OS. For a consistent snapshot, it is recommended you stop the instance and take a snap.
-   If you take a snapshot of an encrypted EBS volume, the snapshot will be encrypted automatically.
-   You can share snapshots, but only in the region in which they were created. To share to other regions, you will need to copy them to the destination region first.

### EBS Encryption -

EBS encrypts your volume with a data key using the industry-standard AES-256 algorithm. Amazon EBS encryption uses AWS Key Management Service (AWS KMS) customer master keys (CMK) when creating encrypted volumes and snapshots.

#### What Happens When You Encrypt an EBS Volume?

-   Data at rest is encrypted inside the volume.
-   All data in flight moving between the instance and the volume is encrypted.
-   All snapshots are encrypted.
-   All volumes created from the snapshot are encrypted.

---

Encryption Explored -

-   Encryption and decryption are handled transparently (you don't need to do anything).
-   Encryption has a minimal
-   Copying an unencrypted snapshot allows encryption.
-   Snapshots of encrypted volumes are encrypted.
-   You can now encrypt root device volumes upon creation.

#### Steps to Encrypt an Unencrypted Volume :

-   Create a snapshot of the unencrypted root device volume.
-   Create a copy of the snapshot and select the encrypt option.
-   Create an AMI from the encrypted snapshot.
-   Use that AMI to launch new encrypted instances.

> We have learned so far we can stop and terminate
> EC2 instances. If we stop the instance, the data is kept on the disk (with EBS) and will remain on the disk until the EC2 instance is started. If the instance is terminated, then by default the root device volume will also be terminated. But we can save it if we want while launching an instance.

#### EC2 Hibernation :

When you hibernate an EC2 instance, the operating system is told to perform hibernation (suspend-to-disk). Hibernation saves the contents from the instance memory (RAM) to your Amazon EBS root volume. We persist the instance's Amazon EBS root volume and any attached Amazon
EBS data volumes.

_When you start your instance out of hibernation:_

-   The Amazon EBS root volume is restored to its previous state.
-   The RAM contents are reloaded.
-   The processes that were previously running on the instance are resumed.
-   Previously attached data volumes are reattached and the instance retains its instance ID.
    ![alt text](/Photos/hibernation.png)

With EC2 hibernation, the instance boots much faster. The operating system does not need to reboot because the in-memory state (RAM) is preserved. This is useful for:

-   Long-running processes
-   Services that take time to initialize

**What You Need to Know about E2C Hibernation**

-   EC2 hibernation preserves the in-memory RAM on persistent storage (EBS).
-   Much faster to boot up because you do not need to reload the operating system.
    V Instance RAM must be less than 150 GB.
-   Instance families include instances in General Purpose, Compute, Memory and Storage Optimized groups.
-   Available for Windows, Amazon Linux 2 AMI, and Ubuntu.
-   Instances can't be hibernated for more than 60 days.
-   Available for On-Demand instances and Reserved Instances.

---

# EFS

-   Managed NFS (network file system) that can be mounted on many EC2 instances.
-   EFS works with EC2 instances in multiple Availability Zones.
-   Highly available and scalable; however, it is expensive.
    ![alt text](/Photos/efs.png)

#### Use Cases :

-   Content Management. Can share content between ec2 instances easily.
-   Great for web servers. Can have a single folder structure for your website.

#### Key Details :

-   The EC2 instances communicate to the remote file system using the NFSv4 protocol. This makes it required to open up the NFS port for our security group (EC2 firewall rules) to allow inbound traffic on that port.
-   Compatible with Linux-based AMI (Windows not supported at this time)
-   Encryption at rest using KMS
-   File system scales automatically; no capacity planning required
-   Pay per use
-   It is best for file storage that is accessed by a fleet of servers rather than just one server

#### EFS Performance :

-   EFS can support thousands of concurrent connections (EC2 instances).
-   EFS can handle up to 10 Gbps in throughput.
-   Scale your storage to petabytes.

#### Controlling Performance :

When creating an EFS file system, you can set what performance characteristics you want.

-   General Purpose : Used for things like web servers, CMS, etc.
-   Max I/O :
    Used for big data, media processing, etc.

### Storage Tiers :

EFS comes with storage tiers and lifecycle management, allowing you to move your data from one tier to another after X number of days.

-   Standard :
    For frequently accessed files
-   Infrequently Accessed :
    For files not
    frequently accessed

### FSx for Windows :

Amazon FSx for Windows File Server provides a fully managed native Microsoft Windows file system so you can easily move your Windows-based applications that require file storage to AWS.

AMAZON FSX IS BUILT ON WINDOWS SERVER.

![alt text](/Photos/fsx.png)

### Amazon FSx for Lustre :

A fully managed file system that is optimized for compute-intensive workloads

-   High Performance Computing
-   Machine Learning
-   Media Data Processing Workflows
-   Electronic Design Automation

### FSx for Lustre Performance

With Amazon FS, you can launch and run a Lustre file system that can process massive datasets at up to hundreds of gigabytes per second of throughput, millions of IOPS, and sub-millisecond latencies.

#### Storage Class Usecases :

-   _EFS_: When you need distributed, highly resilient storage for Linux instances and Linux-based applications.
-   _Amazon FSx for Windows_: When you need centralized storage for Windows-based applications, such as SharePoint, Microsoft SQL Server, Workspaces, IIS Web Server, or any other native Microsoft application.
-   _Amazon FSx for Lustre_: When you need high-speed, high-capacity distributed storage. This will be for applications that do high performance computing (HPC), financial modeling, etc. Remember that FSx for Lustre can store data directly on S3.

### AMI

An Amazon Machine Image (AMI) provides the information required to launch an instance.

_You must specify an AMl when you launch an instance._

#### Things You Can Base Your AMI On -

-   Region
-   Operating system
-   Architecture (32-bit or 64-bit)
-   Launch permissions
-   Storage for the root device (root device volume)

**All AMIs are categorized as either backed by:**

-   _Amazon EBS_ -
    The root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot.
-   _Instance Store_ -
    The root device for an instance launched from the AMl is an instance store volume created from a template stored in Amazon S3.

### Instance Store Volumes -

Instance store volumes are sometimes called ephemeral storage. Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data.
You can, however, reboot the instance without losing your data.

If you delete the instance, you will lose the instance store volume.

### EBS Volumes -

EBS-backed instances can be stopped. You will not lose the data on this instance if it is stopped. You can also reboot an EBS volume and not lose your data.

By default, the root device volume will be deleted on termination. However, you can tell AWS to keep the root device volume with EBS volumes.

> If you use an EBS-backed root volume, the root volume will not be terminated with its EC2 instance when the instance is brought offline. EBS-backed volumes are not temporary storage devices like Instance Store-backed volumes.

### AWS Backup

Backup allows you to consolidate your backups across multiple AWS services, such as EC2, EBS, EFS, Amazon FSx for Lustre, Amazon FSx for Windows File Server, and AWS Storage Gateway.

It can include other services, such as database technologies like RDS and DynamoDB.

> Backup can be used with AWS
> Organizations to back up multiple AWS accounts in your organization.
> It gives you centralized control across all AWS services, in multiple AWS accounts across the entire AWS organization.

**Benefits :**

-   _Central Management_ :
    Use a single, central backup console, allowing you to centralize your backups across multiple AWS services and multiple AWS accounts.
-   _Improved Compliance_ :
    Backup policies can be enforced while backups can be encrypted both at rest and in transit, allowing alignment to regulatory compliance.
    Auditing is made easy due to a consolidated view of backups across many AWS services.
-   _Automation_ :
    You can create automated backup schedules and retention policies. You can also create lifecycle policies, allowing you to expire unnecessary backups after a period of time.

# Databases

## Relational Database Service (RDS)

![alt text](/Photos/rds.png)

Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks.

RDS runs on virtual machines, but you do not have access to those machines. You cannot SSH into an RDS instance so therefore you cannot patch the OS. This means that AWS is responsible for the security and maintenance of RDS. You can provision an EC2 instance as a database if you need or want to manage the underlying server yourself, but not with an RDS engine.

**Relational Database Engines** :

-   SQL Server
-   Oracle
-   MySQL
-   PostgreSQL
-   Maria DB
-   Aurora

**Multi-AZ is supported for all DB flavors except aurora. This is because Aurora is completely fault-tolerant on its own.**

_RDS has two key features when scaling out:_

-   Read replication for improved performance
-   Multi-AZ for high availability
-   Automated backups

> RDS is generally used for Online Transaction Processing (OLTP) workloads.

![alt text](/Photos/oltpvsolap.png)

> With Multi-AZ RDS creates an exact copy of your production database in another AZ.
> ![alt text](/Photos/rdsmultiaz.png)
> RDS will automatically fail over to the standby during a failure so database operations can resume quickly without administrative intervention.

> Multi AZ is for disaster recovery not for performance improvement. i.e you can't pass queries to your standby DB.

_With a Multi-AZ RDS configuration, backups are taken from the standby._

#### Improve RDS Performance :

![alt text](/Photos/readreplica.png)
A read replica is a read-only copy of your primary database.

Great for read-heavy workloads and takes the load off your primary database.

**Details -**

1. With a Read Replica configuration, EC2 connects to the RDS backend using a DNS address and every write that is received by the master database is also passed onto a DB secondary so that it becomes a perfect copy of the master. This has the overall effect of reducing the number of transactions on the master because the secondary DBs can be queried for the same data.
2. However, if the master DB were to fail, there is no automatic failover. You would have to manually create a new connection string to sync with one of the read replicas so that it becomes a master on its own. Then you’d have to update your EC2 instances to point at the read replica. You can have up to five copies of your master DB with read replication.
3. Each Read Replica will have its own DNS endpoint.
4. Automated backups must be enabled in order to use read replicas.
5. You can have read replicas with Multi-AZ turned on or have the read replica in an entirely separate region. You can even have read replicas of read replicas, but watch out for latency or replication lag. The caveat for Read Replicas is that they are subject to small amounts of replication lag. This is because they might be missing some of the latest transactions as they are not updated as quickly as primaries. Application designers need to consider which queries have tolerance to slightly stale data. Those queries should be executed on the read replica, while those demanding completely up-to-date data should run on the primary node.
6. You can promote read replicas to be their very own production database if needed. But it breaks the replication.

## Amazon Aurora

Aurora is the AWS flagship DB known to combine the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases. It is a MySQL/PostgreSQL-compatible RDBMS that provides the security, availability, and reliability of commercial databases at 1/10th the cost of competitors. It is far more effective as an AWS database due to the 5x and 3x performance multipliers for MySQL and PostgreSQL respectively.

**Details :**

-   Start with 10 GB. Scales in 10-GB increments to 128 TB (storage Auto Scaling).
-   Compute resources can scale up to 96 vCPUs and 768 GB of memory.
-   2 copies of your data are contained in each Availability Zone, with a minimum of 3 Availability Zones. 6 copies of your data.
-   Amazon Aurora typically involves a cluster of DB instances instead of a single instance. Each connection is handled by a specific DB instance. When you connect to an Aurora cluster, the host name and port that you specify point to an intermediate handler called an endpoint. Aurora uses the endpoint mechanism to abstract these connections. Thus, you don't have to hard code all the host names or write your own logic for load-balancing and rerouting connections when some DB instances aren't available.
-   Automated backups are always enabled on Aurora instances and backups don’t impact DB performance. You can also take snapshots which also don’t impact performance. Your snapshots can be shared across AWS accounts.

**Scaling Aurora** :

-   Aurora is designed to transparently handle the loss of up to 2 copies of data without affecting database write availability and up to 3 copies without affecting read availability.
-   Aurora storage is also self-healing. Data blocks and disks are continuously scanned for errors and repaired automatically.

_Types of Aurora Replicas available -_
![alt text](/Photos/aurora-replica.png)

![alt text](/Photos/image3.png)

### Amazon Aurora Serverless

An on-demand, auto-scaling configuration for the MySQL-compatible and PostgreSQL-compatible editions of Amazon Aurora. An Aurora Serverless DB cluster automatically starts up, shuts down, and scales capacity up or down based on your application's needs.

## DynamoDB

Amazon DynamoDB is a key-value and document database that delivers single-digit millisecond performance at any scale. It's a fully managed, multiregion, multimaster, durable non-SQL database. It comes with built-in security, backup and restore, and in-memory caching for internet-scale applications.

**DynamoDB Key Details:**

-   The main components of DynamoDB are:

    -   a collection which serves as the foundational table
    -   a document which is equivalent to a row in a SQL database
    -   key-value pairs which are the fields within the document or row

-   The convenience of non-relational DBs is that each row can look entirely different based on your use case. There doesn't need to be uniformity. For example, if you need a new column for a particular entry you don't also need to ensure that that column exists for the other entries.

-   Stored on SSD storage
-   Spread across 3 geographically distinct data centers
-   Eventually consistent reads (by default)
-   Strongly consistent reads

The difference between the two consistency models is the one second rule. With Eventual Consistent Reads, all copies of data are usually identical within one second after a write operation. A repeated read after a short period of time should return the updated data. However, if you need to read updated data within or less than a second and this needs to be a guarantee, then strongly consistent reads are your best bet.

-   DynamoDB supports both document and key-value based models. It is a great fit for mobile, web, gaming, ad-tech, IoT, etc.

-   If you face a scenario that requires the schema, or the structure of your data, to change frequently, then you have to pick a database which provides a non-rigid and flexible way of adding or removing new types of data. This is a classic example of choosing between a relational database and non-relational (NoSQL) database. In this scenario, pick DynamoDB.

-   A relational database system does not scale well for the following reasons:

    -   It normalizes data and stores it on multiple tables that require multiple queries to write to disk.
    -   It generally incurs the performance costs of an ACID-compliant transaction system.
    -   It uses expensive joins to reassemble required views of query results.

-   High cardinality is good for DynamoDB I/O performance. The more distinct your partition key values are, the better. It makes it so that the requests sent will be spread across the partitioned space.
-   DynamoDB makes use of parallel processing to achieve predictable performance. You can visualize each partition or node as an independent DB server of fixed size with each partition or node responsible for a defined block of data. In SQL terminology, this concept is known as sharding but of course DynamoDB is not a SQL-based DB. With DynamoDB, data is stored on Solid State Drives (SSD).

### DynamoDB Accelerator (DAX):

-   Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache that can reduce Amazon DynamoDB response times from milliseconds to microseconds, even at millions of requests per second.
-   No need for developers to manage caching logic.
    ![alt text](/Photos/image4.png)
-   Pay-per-request pricing
-   Balance cost and performance
-   No minimum capacity
-   Pay more per request than with provisioned capacity
-   Used for new product launches
-   Encyption at rest using KMS
-   Can connect to dynamo DB using a site-to-site VPN and also can use direct connect.

![alt text](/Photos/image5.png)

> With dynamoDB you cannot make concurrent updates to multiple tables at the same time
> and with dynamoDB transactions you're able to do exactly that.

**DynamoDB transactions** provide developers atomicity, consistency, isolation, and durability
(ACID) across 1 or more tables within a single AWS account and region.
You can use transactions when building applications that require coordinated inserts, deletes, or updates to multiple items as part of a single logical business operation.

### On-Demand Backup and Restore -

-   Full backups at any time
-   Zero impact on table performance or availability
-   Consistent within seconds and retained until deleted
-   Operates within same region as the source table

### Point-in-Time Recovery (PITR) -

-   Protects against accidental writes or deletes
-   Restore to any point in the last 35 days
-   Incremental backups
-   Not enabled by default
-   Latest restorable: 5 minutes in the past

### DynamoDB Streams:

![alt text](/Photos/image6.png)
A DynamoDB stream is an ordered flow of information about changes to items in an Amazon DynamoDB table. When you enable a stream on a table, DynamoDB captures information about every modification to data items in the table.

-   Amazon DynamoDB is integrated with AWS Lambda so that you can create triggers—pieces of code that automatically respond to events in DynamoDB Streams.
-   Immediately after an item in the table is modified, a new record appears in the table's stream. AWS Lambda polls the stream and invokes your Lambda function synchronously when it detects new stream records. The Lambda function can perform any actions you specify, such as sending a notification or initiating a workflow.
-   With triggers, you can build applications that react to data modifications in DynamoDB tables.
-   Whenever an application creates, updates, or deletes items in the table, DynamoDB Streams writes a stream record with the primary key attribute(s) of the items that were modified. A stream record contains information about a data modification to a single item in a DynamoDB table. You can configure the stream so that the stream records capture additional information, such as the "before" and "after" images of modified items.

### DynamoDB Global Tables :

Global Tables is a multi-region, multi-master replication solution for fast local performance of globally distributed apps.
Global Tables replicates your Amazon DynamoDB tables automatically across your choice of AWS regions.

-   It is based on DynamoDB streams and is multi-region redundant for data recovery or high availability purposes. Application failover is as simple as redirecting your application’s DynamoDB calls to another AWS region.
-   Global Tables eliminates the difficult work of replicating data between regions and resolving update conflicts, enabling you to focus on your application’s business logic. You do not need to rewrite your applications to make use of Global Tables.
-   Replication latency with Global Tables is typically under one second.
-   To create a global table you need global streams turned on.

### Operating MongoDB-Compatible Databases in Amazon DocumentDB :

MongoDB is a document database that allows for scalability and flexibility with your data as well as robust querying and indexing features.

### Amazon DocumentDB

Allows you to run MongoDB on the AWS cloud. It's a managed database service that scales with your workloads and safely and durably stores your database information.

![alt text](/Photos/image7.png)

**UseCase -**

You no longer have to worry about all the manual tasks when running MongoDB workloads, such as cluster management software, configuring backups, or monitoring production workloads.

_Get rid of your operational overheads!_

### Cassandra

A distributed database (i.e., it runs on many machines) that uses NoSQL. It's primarily used for big data solutions.

Enterprises, such as Netflix, use Cassandra on their backend.

### Amazon Keyspaces

![alt text](/Photos/image8.png)
Amazon's Apache Cassandra database service. It allows you to run Cassandra workloads on AWS and is a fully managed database service.

-   It's a fully managed database service - you don't need to worry about managing servers, software, patching, etc.
-   Keyspaces is serverless!
-   You pay for only the resources you use, and the service can automatically scale tables up and down in response to your applications.

### Graph Database

A graph database stores nodes and relationships instead of tables or documents.

### Neptune

_Neptune is Amazon's graph database service._

Neptune is a fast, reliable, fully managed graph database service that makes it easy to build and run applications.

**Use Cases for Neptune :**

-   Easily build identity graphs for identity resolution solutions such as social graphs, and accelerate updates for ad targeting, personalization, and analytics.
-   Add topical data to product catalogs, model general information, and help users quickly navigate highly connected datasets.
-   Build graph queries for near real-time identity fraud pattern detection in financial and purchase transactions.
-   Proactively detect and investigate IT
    infrastructure using a layered security approach.
    Visualize all infrastructure to plan, predict, and mitigate risk.

### Ledger Database

It's a NoSQL database that is immutable, transparent, and has a cryptographically verifiable transaction log that is owned by one authority.

You cannot update a record (i.e., replace old content) in a ledger database. Instead, an update adds a new record to the database.

-   It's used for
    cryptocurrencies, such as Bitcoin, Ethereum, etc.
-   Shipping companies use it to track items, boxes, shipping containers, deliveries, etc.
-   Pharmaceutical companies use it to track creation and distribution of drugs and ensure no counterfeits are produced.

### Amazon Quantum Ledger Database (QLDB)

![alt text](/Photos/image9.png)

A fully managed ledger database that provides a transparent, immutable, and cryptographically verifiable transaction log.

**QLD Use Cases** :

-   Create a complete and accurate record of all financial transactions, such as credit and debit transactions.
-   Record the history of each transaction, and provide details of every batch manufactured, shipped, stored, and sold from facility to store.
-   Track a claim over its lifetime, and cryptographically verify data integrity to make the application resilient against data entry errors and manipulation.
-   Implement a system-of-record application tocreate a complete, centralized record of employee details, such as payroll, bonus, and benefits.

### Time-Series Data

Data points that are logged over a series of time, allowing you to track your data. Examples could be temperature readings from weather stations around the world, on the hour, every hour for years.

_Time-Series Data Examples :_

-   IoT sensors relay thousands, millions, and billions of points of information depending on the setup. One use case is for agriculture.
-   Large websites such as Netflix serve millions of users per second. Need to analyze incoming and outgoing web traffic.
-   Applications that change in response to users needs may need to be monitored continuously so they can scale correctly.

### Amazon Timestream

![alt text](/Photos/image10.png)

A serverless, fully managed database service for time-series data. You can analyze trillions of events per day up to 1,000 times faster and at as little as
1/10th the cost of traditional relational databases.

---

# Virtual Private Cloud (VPC) Networking

With Amazon Virtual Private Cloud (Amazon VPC), you can launch AWS resources in a logically isolated virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS. By having the option of selecting which AWS resources are public facing and which are not, VPC provides much more granular control over security.

![alt text](/Photos/image12.png)

_You get a default VPC in every region in your AWS account._

-   You can think of VPC as your own virtual data center in the cloud. You have complete control of your own network; including the IP range, the creation of sub-networks (subnets), the configuration of route tables and the network gateways used.

-   You can create a hardware Virtual Private Network (VPN) connection between your corporate data center and your VPC and leverage the AWS Cloud as an extension of your corporate data center.

**Network Diagram :**
![alt text](/Photos/image11.png)

### VPC Details -

-   Launch instances into a subnet of your choosing.
-   Assign custom IP address ranges in each subnet.
-   Configure route tables between subnets.
-   Create internet gateway and attach it to our VPC.
-   Much better security control over your AWS resources.
-   Subnet network access control lists.
-   _You can use network access control lists (NACLs) to block specific IP addresses._

### Features --

-   **Subnets** :
    If a network has a large number of hosts without logically grouped subdivisions, managing the many hosts can be a tedious job. Therefore you use subnets to divide a network so that management becomes easier.
-   **IP addressing** :
    You can assign IP addresses, both IPv4 and IPv6, to your VPCs and subnets. You can also bring your public IPv4 addresses and IPv6 GUA addresses to AWS and allocate them to resources in your VPC, such as EC2 instances, NAT gateways, and Network Load Balancers.

-   **Routing** :
    Use route tables to determine where network traffic from your subnet or gateway is directed.

-   **Gateways and endpoints** :
    A gateway connects your VPC to another network. For example, use an internet gateway to connect your VPC to the internet. Use a VPC endpoint to connect to AWS services privately, without the use of an internet gateway or NAT device.

-   **Peering connections** :
    Use a VPC peering connection to route traffic between the resources in two VPCs.

-   **Traffic Mirroring** :
    Copy network traffic from network interfaces and send it to security and monitoring appliances for deep packet inspection.

-   **Transit gateways** :Use a transit gateway, which acts as a central hub, to route traffic between your VPCs, VPN connections, and AWS Direct Connect connections.

-   **VPC Flow Logs** :
    A flow log captures information about the IP traffic going to and from network interfaces in your VPC.

-   **VPN connections** :
    Connect your VPCs to your on-premises networks using AWS Virtual Private Network (AWS VPN).

> Amazon always reserves five IP addresses within a subnet. The first four IP addresses and the last IP address of each subnet CIDR block will always be unavailable for use.

### NAT Gateways :

You can use a network address translation (NAT) gateway to enable instances in a private subnet to connect to the internet or other AWS services while preventing the internet from initiating a connection with those instances.

-   Redundant inside the Availability Zone
-   Starts at 5 Gbps and scales currently to 45 Gbps
-   No need to patch
-   Not associated with security groups
-   Automatically assigned a public IP address

![alt text](/Photos/image13.png)

### Network Access Control Lists:

Network Access Control Lists (or NACLs) are like security groups but for subnets rather than instances. The main difference between security groups and NACLs is that security groups are stateful, meaning you can perform both allow and deny rules that may be divergent, depending if traffic is inbound or outbound, for that rule.

| NACL                                                                                                                                                                                   | Security Group                                                                                                                                               |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Operates at the subnet level                                                                                                                                                           | Operates at the instance level                                                                                                                               |
| Supports allow rules and deny rules                                                                                                                                                    | Supports allow rules only                                                                                                                                    |
| Is stateless: Return traffic must be explicitly allowed by rules                                                                                                                       | Is stateful: Return traffic is automatically allowed, regardless of any rules                                                                                |
| We process rules in order, starting with the lowest numbered rule, when deciding whether to allow traffic                                                                              | We evaluate all rules before deciding whether to allow traffic                                                                                               |
| Automatically applies to all instances in the subnets that it's associated with (therefore, it provides an additional layer of defense if the security group rules are too permissive) | Applies to an instance only if someone specifies the security group when launching the instance, or associates the security group with the instance later on |

-   Because NACLs are stateless, you must also ensure that outbound rules exist alongside the inbound rules so that ingress and egress can flow smoothly.

-   The default NACL that comes with a new VPC has a default rule to allow all inbounds and outbounds. This means that it exists, but doesn't do anything as all traffic passes through it freely.

    However, when you create a new NACL (instead of using the default that comes with the VPC) the default rules will deny all inbounds and outbounds.

-   NACLs are evaluated before security groups and you block malicious IPs with NACLs, not security groups.
-   You can associate a network ACL with multiple subnets; however, a subnet can be associated with only 1 network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.
-   Network ACLs contain a numbered list of rules that are evaluated in order, starting with the lowest numbered rule.

#### NAT Instances vs. NAT Gateways:

Attaching an Internet Gateway to a VPC allows instances with public IPs to directly access the internet. NAT does a similar thing, however it is for instances that do not have a public IP. It serves as an intermediate step which allow private instances to first mask their own private IP as the NAT's public IP before accessing the internet.

You would want your private instances to access the internet so that they can have normal software updates. NAT prevents any initiating of a connection from the internet.

NAT instances are individual EC2 instances that perform the function of providing private subnets a means to securely access the internet.

Because they are individual instances, High Availability is not a built-in feature and they can become a choke point in your VPC. They are not fault-tolerant and serve as a single point of failure. While it is possible to use auto-scaling groups, scripts to automate failover, etc. to prevent bottlenecking, it is far better to use the NAT Gateway as an alternative for a scalable solution.

NAT Gateway is a managed service that is composed of multiple instances linked together within an availability zone in order to achieve HA by default.

To achieve further HA and a zone-independent architecture, create a NAT gateway for each Availability Zone and configure your routing to ensure that resources use the NAT gateway in their corresponding Availability Zone.

NAT instances are deprecated, but still useable. NAT Gateways are the preferred means to achieve Network Address Translation.

There is no need to patch NAT Gateways as the service is managed by AWS. You do need to patch NAT Instances though because they’re just individual EC2 instances.

Because communication must always be initiated from your private instances, you need a route rule to route traffic from a private subnet to your NAT gateway.

Your NAT instance/gateway will have to live in a public subnet as your public subnet is the subnet configured to have internet access.

When creating NAT instances, it is important to remember that EC2 instances have source/destination checks on them by default. What these checks do is ensure that any traffic it comes across must be either generated by the instance or be the intended recipient of that traffic. Otherwise, the traffic is dropped because the EC2 instance is neither the source nor the destination.

So because NAT instances act as a sort of proxy, you must disable source/destination checks when musing a NAT instance.

### Route Tables:

Route tables are used to make sure that subnets can communicate with each other and that traffic knows where to go.

Every subnet that you create is automatically associated with the main route table for the VPC.

You can have multiple route tables. If you do not want your new subnet to be associated with the default route table, you must specify that you want it associated with a different route table.

Because of this default behavior, there is a potential security concern to be aware of: if the default route table is public then the new subnets associated with it will also be public.

The best practice is to ensure that the default route table where new subnets are associated with is private.

This means you ensure that there is no route out to the internet for the default route table. Then, you can create a custom route table that is public instead. New subnets will automatically have no route out to the internet. If you want a new subnet to be publicly accessible, you can simply associate it with the custom route table.

Route tables can be configured to access endpoints (public services accessed privately) and not just the internet.

### Subnets :

A subnet is a range of IP addresses in your VPC. A subnet must reside in a single Availability Zone. After you add subnets, you can deploy AWS resources in your VPC.

Each subnet must reside entirely within one Availability Zone and cannot span zones. By launching AWS resources in separate Availability Zones, you can protect your applications from the failure of a single Availability Zone.

The idea of subnetting is to take a portion of the host space of an address, and use it as an additional networking specification to divide the address space again.

### Internet Gateway:

If the Internet Gateway is not attached to the VPC, which is the prerequisite for instances to be accessed from the internet, then naturally instances in your VPC will not be reachable.

If you want all of your VPC to remain private (and not just some subnets), then do not attach an IGW.

When a Public IP address is assigned to an EC2 instance, it is effectively registered by the Internet Gateway as a valid public endpoint. However, each instance is only aware of its private IP and not its public IP. Only the IGW knows of the public IPs that belong to instances.

When an EC2 instance initiates a connection to the public internet, the request is sent using the public IP as its source even though the instance doesn't know a thing about it. This works because the IGW performs its own NAT translation where private IPs are mapped to public IPs and vice versa for traffic flowing into and out of the VPC.

So when traffic from the internet is destined for an instance's public IP endpoint, the IGW receives it and forwards the traffic onto the EC2 instance using its internal private IP.

You can only have one IGW per VPC.

**Summary: IGW connects your VPC with the internet.**
A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.

_Instances in your VPC do not require public IP addresses to communicate with resources in the service._

Traffic between your VPC and the other service does not leave the Amazon network.

**Endpoints Are Virtual Devices.**
They are horizontally scaled, redundant, and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.

Types of Endpoints :

-   INTERFACE ENDPOINTS : Interface Endpoints use AWS PrivateLink and have a private IP address so they are their own entity and not just a target in a route table. Because of this, they cost $.01/hour. Gateway Endpoints are free as they’re just a new route in to set.

-   GATEWAY ENDPOINTS :
    Gateway Endpoints rely on creating entries in a route table and pointing them to private endpoints used for S3 or DynamoDB. Gateway Endpoints are mainly just a target that you set.

**Summary: VPC Endpoints connect your VPC with AWS services through a non-public tunnel.**

### Multiple VPCs

Sometimes you may need to have several VPCs for different environments, and it may be necessary to connect these VPCs to each other.

![alt text](/Photos/image14.png)

That's what VPC Peering is all about -

### VPC Peering:

VPC peering allows you to connect one VPC with another via a direct network route using the Private IPs belonging to both. With VPC peering, instances in different VPCs behave as if they were on the same network.

You can create a VPC peering connection between your own VPCs, regardless if they are in the same region or not, and with a VPC in an entirely different AWS account.

VPC Peering is usually done in such a way that there is one central VPC that peers with others. Only the central VPC can talk to the other VPCs.

You cannot do transitive peering for non-central VPCs. Non-central VPCs cannot go through the central VPC to get to another non-central VPC. You must set up a new portal between non-central nodes if you need them to talk to each other.
![alt text](/Photos/image16.png)

The following diagram highlights the above idea. VPC B is free to communicate with VPC A with VPC Peering enabled between both. However, VPC B cannot continue the conversation with VPC C. Only VPC A can communicate with VPC C.

![alt text](/Photos/image15.png)

It is worth knowing what VPC peering configurations are not supported:

-   Overlapping CIDR Blocks
-   Transitive Peering
-   Edge to Edge Routing through a gateway or connection device (VPN connection, Internet Gateway, AWS Direct Connect connection, etc.)

You can peer across regions, but you cannot have one subnet stretched over multiple availability zones. However, you can have multiple subnets in the same availability zone.

**Summary: VPC Peering connects your VPC to another VPC through a non-public tunnel.**

### AWS PrivateLink:

AWS PrivateLink simplifies the security of data shared with cloud-based applications by eliminating the exposure of data to the public Internet. AWS PrivateLink provides private connectivity between different VPCs, AWS services, and on-premises applications, securely on the Amazon network.

It's similar to the AWS Direct Connect service in that it establishes private connections to the AWS cloud, except Direct Connect links on-premises environments to AWS. PrivateLink, on the other hand, secures traffic from VPC environments which are already in AWS.

This is useful because different AWS services often talk to each other over the internet. If you do not want that behavior and instead want AWS services to only communicate within the AWS network, use AWS PrivateLink. By not traversing the Internet, PrivateLink reduces the exposure to threat vectors such as brute force and distributed denial-of-service attacks.

PrivateLink allows you to publish an "endpoint" that others can connect with from their own VPC. It's similar to a normal VPC Endpoint, but instead of connecting to an AWS service, people can connect to your endpoint.

Further, you'd want to use private IP connectivity and security groups so that your services function as though they were hosted directly on your private network.

Remember that AWS PrivateLink applies to Applications/Services communicating with each other within the AWS network. For VPCs to communicate with each other within the AWS network, use VPC Peering.

**Summary: AWS PrivateLink connects your AWS services with other AWS services through a non-public tunnel.**

### Virtual Private Networks (VPNs):

VPCs can also serve as a bridge between your corporate data center and the AWS cloud. With a VPC Virtual Private Network (VPN), your VPC becomes an extension of your on-prem environment.

Naturally, your instances that you launch in your VPC can't communicate with your own on-premise servers. You can allow the access by first:

-   attaching a virtual private gateway to the VPC
-   creating a custom route table for the connection
-   updating your security group rules to allow traffic from the connection
-   creating the managed VPN connection itself.

To bring up VPN connection, you must also define a customer gateway resource in AWS, which provides AWS information about your customer gateway device. And you have to set up an
Internet-routable IP address of the customer gateway's external interface.

A customer gateway is a physical device or software application on the on-premise side of the VPN connection.

Although the term "VPN connection" is a general concept, a VPN connection for AWS always refers to the connection between your VPC and your own network. AWS supports Internet Protocol security (IPsec) VPN connections.

The following diagram illustrates a single VPN connection :
![alt text](/Photos/image17.png)

The above VPC has an attached virtual private gateway (note: not an internet gateway) and there is a remote network that includes a customer gateway which you must configure to enable the VPN connection. You set up the routing so that any traffic from the VPC bound for your network is routed to the virtual private gateway.

_VGW is a VPN concentrator on the AWS side of the VPN connection between two networks. It is part of a VPC and provides edge routing for AWS managed VPN connections and AWS Direct Connect connections._

**Summary: VPNs connect your on-prem with your VPC over the internet.**

#### AWS VPN CloudHub -

If you have multiple sites, each with its own VPN connection, you can use AWS VPN CloudHub to connect those sites together.

-   Hub-and-spoke model
-   Low cost and easy to manage
-   It operates over the public internet, but all traffic between the customer gateway and the AWS VPN CloudHub is encrypted.

AWS VPN CloudHub is low cost and easy to manage. Though it operates over the public internet, all traffic between the customer gateway and the AWS VPN CloudHub is encrypted.

### AWS DirectConnect:

Direct Connect is an AWS service that establishes a dedicated network connection between your premises and AWS. You can create this private connectivity to reduce network costs, increase bandwidth, and provide more consistent network experience compared to regular internet-based connections.

2 Types of Direct Connect Connection :

-   _Dedicated Connection_: A physical
    Ethernet connection associated with a single customer. Customers can request a dedicated connection through the AWS Direct Connect console, the CLI, or the API.

-   _Hosted Connection_: A physical Ethernet
    connection that an AWS Direct Connect
    Partner provisions on behalf of a customer. Customers request a hosted connection by contacting a partner in the AWS Direct Connect Partner Program, who provisions the connection.

The use case for Direct Connect is high throughput workloads or if you need a stable or reliable connection

VPN connects to your on-prem over the internet and DirectConnect connects to your on-prem off through a private tunnel.

The steps for setting up an AWS DirectConnect connection:

-   Create a virtual interface in the DirectConnect console. This is a public virtual interface.
-   Go to the VPC console and then VPN connections. Create a customer gateway for your on-premise.
-   Create a virtual private gateway and attach it to the desired VPC environment.
-   Select VPN connections and create a new VPN connection. Select both the customer gateway and the virtual private gateway.
-   Once the VPN connection is available, set up the VPN either on the customer gateway or the on-prem firewall itself

Data flow into AWS via DirectConnect looks like the following: On-prem router -> dedicated line -> your own cage / DMZ -> cross connect line -> AWS Direct Connect Router -> AWS backbone -> AWS Cloud

![alt text](/Photos/image18.png)

**Summary: DirectConnect connects your on-prem with your VPC through a non-public tunnel.**

> VPNs vs. Direct Connect:
>
> VPNs allow private communication, but it still traverses the public internet to get the data delivered. While secure, it can be painfully slow.
>
> DIRECT CONNECT IS:
>
> -   Fast
> -   Secure
> -   Reliable
> -   Able to take massive throughput

### Transit Gateway

AWS Transit Gateway connects VPCs and on-premises networks through a central hub. This simplifies your network and puts an end to complex peering relationships. It acts as a cloud router - each new connection is only made once.

![alt text](/Photos/image19.png)

-   Allows you to have transitive peering between thousands of VPCs and on-premises data centers.
-   Works on a hub-and-spoke model.
-   Works on a regional basis, but you can have it across multiple regions.
-   You can use it across multiple AWS accounts using RAM (Resource Access Manager).

#### 5G Networks

5G provides mobile devices with higher speed, lower latency, and greater capacity than 4G LTE networks. It is one of the fastest, most robust technologies the world has ever seen.

### AWS Wavelength

AWS Wavelength embeds AWS
compute and storage services within
5G networks, providing mobile edge computing infrastructure for developing, deploying, and scaling ultra-low-latency applications.

---

# Route53

Amazon Route 53 is a highly available and scalable Domain Name System (DNS) service. You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking.

### Details -

DNS is used to map human-readable domain names into an internet protocol address similarly to how phone books map company names with phone numbers.

AWS has its own domain registrar.

When you buy a domain name, every DNS address starts with an SOA (Start of Authority) record. The SOA record stores information about the name of the server that kicked off the transfer of ownership, the administrator who will now use the domain, the current metadata available, and the default number of seconds or TTL.

NS records, or Name Server records, are used by the Top Level Domain hosts (.org, .com, .uk, etc.) to direct traffic to the Content servers. The Content DNS servers contain the authoritative DNS records.

Browsers talk to the Top Level Domains whenever they are queried and encounter domain name that they do not recognize.

-   Browsers will ask for the authoritative DNS records associated with the domain.
-   Because the Top Level Domain contains NS records, the TLD can in turn query the Name Servers for their own SOA.
-   Within the SOA, there will be the requested information.
-   Once this information is collected, it will then be returned all the way back to the original browser asking for it.

**In summary: Browser -> TLD -> NS -> SOA -> DNS record. The pipeline reverses when the correct DNS record is found.**

Authoritative name servers store DNS record information, usually a DNS hosting provider or domain registrar like GoDaddy that offers both DNS registration and hosting.

There are a multitude of DNS records for Route53. Here are some of the more common ones:

-   **A records** : These are the fundamental type of DNS record. The “A” in A records stands for “address”. These records are used by a computer to directly pair a domain name to an IP address. IPv4 and IPv6 are both supported with "AAAA" referring to the IPv6 version. A: URL -> IPv4 and AAAA: URL -> IPv6.
-   **CName records** : Also referred to as the Canonical Name. These records are used to resolve one domain name to another domain name. For example, the domain of the mobile version of a website may be a CName from the domain of the browser version of that same website rather than a separate IP address. This would allow mobile users who visit the site and to receive the mobile version. CNAME: URL -> URL.
-   **Alias records** : These records are used to map your domains to AWS resources such as load balancers, CDN endpoints, and S3 buckets. Alias records function similarly to CNames in the sense that you map one domain to another. The key difference though is that by pointing your Alias record at a service rather than a domain name, you have the ability to freely change your domain names if needed and not have to worry about what records might be mapped to it. Alias records give you dynamic functionality. Alias: URL -> AWS Resource.
-   **PTR records** : These records are the opposite of an A record. PTR records map an IP to a domain and they are used in reverse DNS lookups as a way to obtain the domain name of an IP address. PTR: IPv4 -> URL.

One other major difference between CNames and Alias records is that a CName cannot be used for the naked domain name (the apex record in your entire DNS configuration / the primary record to be used). CNames must always be secondary records that can map to another secondary record or the apex record. The primary must always be of type Alias or A Record in order to work.

Due to the dynamic nature of Alias records, they are often recommended for most use cases and should be used when it is possible to.

TTL is the length that a DNS record is cached on either the resolving servers or the users own cache so that a fresher mapping of IP to domain can be retrieved. Time To Live is measured in seconds and the lower the TTL the faster DNS changes propagate across the internet. Most providers, for example, have a TTL that lasts 48 hours.

You can create health checks to send you a Simple Notification if any issues arise with your DNS setup.

Further, Route53 health checks can be used for any AWS endpoint that can be accessed via the Internet. This makes it an ideal option for monitoring the health of your AWS endpoints.

## Route53 Routing Policies:

When you create a record, you choose a routing policy, which determines how Amazon Route 53 responds to DNS queries. The routing policies available are:

-   Simple Routing
-   Weighted Routing
-   Latency-based Routing
-   Failover Routing
-   Geolocation Routing
-   Geo-proximity Routing
-   Multivalue Answer Routing

**Simple Routing** is used when you just need a single record in your DNS with either one or more IP addresses behind the record in case you want to balance load. If you specify multiple values in a Simple Routing policy, Route53 returns a random IP from the options available.

![alt text](/Photos/image20.png)

**Weighted Routing** is used when you want to split your traffic based on assigned weights. For example, if you want 80% of your traffic to go to one AZ and the rest to go to another, use Weighted Routing. This policy is very useful for testing feature changes and due to the traffic splitting characteristics, it can double as a means to perform blue-green deployments. When creating Weighted Routing, you need to specify a new record for each IP address. You cannot group the various IPs under one record like with Simple Routing.

**Latency-based Routing**, as the name implies, is based on setting up routing based on what would be the lowest latency for a given user. To use latency-based routing, you must create a latency resource record set in the same region as the corresponding EC2 or ELB resource receiving the traffic. When Route53 receives a query for your site, it selects the record set that gives the user the quickest speed. When creating Latency-based Routing, you need to specify a new record for each IP.
![alt text](/Photos/image23.png)

**Failover Routing** is used when you want to configure an active-passive failover set up. Route53 will monitor the health of your primary so that it can failover when needed. You can also manually set up health checks to monitor all endpoints if you want more detailed rules.
![alt text](/Photos/image21.png)

**Geolocation Routing** lets you choose where traffic will be sent based on the geographic location of your users.
![alt text](/Photos/image22.png)

**Geo-proximity Routing** lets you choose where traffic will be sent based on the geographic location of your users and your resources. You can choose to route more or less traffic based on a specified weight which is referred to as a bias. This bias either expands or shrinks the availability of a geographic region which makes it easy to shift traffic from resources in one location to resources in another. To use this routing method, you must enable Route53 traffic flow. If you want to control global traffic, use Geo-proximity routing. If you want traffic to stay in a local region, use Geolocation routing.

**Multivalue Routing** is pretty much the same as Simple Routing, but Multivalue Routing allows you to put health checks on each record set. This ensures then that only a healthy IP will be randomly returned rather than any IP.
![alt text](/Photos/image24.png)

---

# Elastic Load Balancers (ELB)

Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, Docker containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones. Elastic Load Balancing offers three types of load balancers that all feature the high availability, automatic scaling, and robust security necessary to make your applications fault tolerant.

![alt text](/Photos/image25.png)

-   Load balancers can be internet facing or application internal.
-   To route domain traffic to an ELB load balancer, use Amazon Route 53 to create an Alias record that points to your load balancer. An Alias record is preferable over a CName, but both can work.
-   ELBs do not have predefined IPv4 addresses; you must resolve them with DNS instead. Your load balancer will never have its own IP by default, but you can create a static IP for a network load balancer because network LBs are for high performance purposes.
-   Instances behind the ELB are reported as InService or OutOfService. When an EC2 instance behind an ELB fails a health check, the ELB stops sending traffic to that instance.
-   A dual stack configuration for a load balancer means load balancing over IPv4 and IPv6

_In AWS, there are four types of LBs :_

-   **Application LBs** : Application LBs are best suited for HTTP(S) traffic and they balance load on layer 7 OSI. They are intelligent enough to be application aware and Application Load Balancers also support path-based routing, host-based routing and support for containerized applications. As an example, if you change your web browser’s language into French, an Application LB has visibility of the metadata it receives from your browser which contains details about the language you use. To optimize your browsing experience, it will then route you to the French-language servers on the backend behind the LB. You can also create advanced request routing, moving traffic into specific servers based on rules that you set yourself for specific cases.

-   **Network LBs** : Network LBs are best suited for TCP traffic where performance is required and they balance load on layer 4. They are capable of managing millions of requests per second while maintaining extremely low latency.

-   **Classic LBs** : Classic LBs are the legacy ELB product and they balance either on HTTP(S) or TCP, but not both. Even though they are the oldest LBs, they still support features like sticky sessions and X-Forwarded-For headers.

-   **Gateway Load Balancer** : Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, in one or more Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer as your incoming traffic changes over time. It can automatically scale to the vast majority of workloads.

![alt text](/Photos/image26.png)

_The lifecycle of a request to view a website behind an ELB:_

-   The browser requests the IP address for the load balancer from DNS.
-   DNS provides the IP.
-   With the IP at hand, your browser then makes an HTTP request for an HTML page from the Load Balancer.
-   AWS perimeter devices checks and verifies your request before passing it onto the LB.
-   The LB finds an active webserver to pass on the HTTP request.
-   The webserver returns the requested HTML file.
-   The browser receives the HTML file it requested and renders the graphical representation of it on the screen.
-   Load balancers are a regional service. They do not balance load across different regions. You must provision a new ELB in each region that you operate out of.
-   If your application stops responding, you’ll receive a 504 error when hitting your load balancer. This means the application is having issues and the error could have bubbled up to the load balancer from the services behind it. It does not necessarily mean there's a problem with the LB itself.

### ELB Advanced Features:

-   To enable IPv6 DNS resolution, you need to create a second DNS resource record so that the ALIAS AAAA record resolves to the load balancer along with the IPv4 record.
-   The X-Forwarded-For header, via the Proxy Protocol, is simply the idea for load balancers to forward the requester's IP address along with the actual request for information from the servers behind the LBs. Normally, the servers behind the LBs only see that the IP sending it traffic belongs to the Load Balancer. They usually have no idea about the true origin of the request as they only know about the computer (the LB) that asks them to do something. But sometimes we may want to route the original IP to the backend servers for specific use cases and have the LB’s IP address ignored. The X-Forwarded-For header makes this possible.
-   Sticky Sessions bind a given user to a specific instance throughout the duration of their stay on the application or website. This means all of their interactions with the application will be directed to the same host each time. If you need local disk for your application to work, sticky sessions are great as users are guaranteed consistent access to the same ephemeral storage on a particular instance. The downside of sticky sessions is that, if done improperly, it can defeat the purpose of load balancing. All traffic could hypothetically be bound to the same instance instead of being evenly distributed.
-   Path Patterns create a listener with rules to forward requests based on the URL path set within those user requests. This method, known as path-based routing, ensures that traffic can be specifically directed to multiple back-end services. For example, with Path Patterns you can route general requests to one target group and requests to render images to another target group. So the URL, “www.example.com/” will be forwarded to a server that is used for general content while “www.example.com/photos” will be forwarded to another server that renders images.

**Gateway Timeouts** -
If your application stops responding, the Classic Load Balancer responds with a 504 error.

This means the application is having issues. This could be either at the web server layer or database layer.

**Deregistration Delay** -

_Enable deregistration delay_ : Keep existing connections open if the EC2 instance becomes unhealthy.

_Disable Enable deregistration delay_ : Do this if you want your load balancer to immediately close connections to the instances that are de-registering or have become unhealthy.

### ELB Cross Zone Load Balancing:

-   Cross Zone load balancing guarantees even distribution across AZs rather than just within a single AZ.
-   If Cross Zone load balancing is disabled, each load balancer node distributes requests evenly across the registered instances in its Availability Zone only.
-   Cross Zone load balancing reduces the need to maintain equivalent numbers of instances in each enabled Availability Zone, and improves your application's ability to handle the loss of one or more instances.
-   However, it is still recommend that you maintain approximately equivalent numbers of instances in each enabled Availability Zone for higher fault tolerance.
-   For environments where clients cache DNS lookups, incoming requests might favor one of the Availability Zones. Using Cross Zone load balancing, this imbalance in the request load is spread across all available instances in the region instead.

### ELB Security:

-   ELB supports SSL/TLS & HTTPS termination. Termination at load balancer is desired because decryption is resource and CPU intensive. Putting the decryption burden on the load balancer enables the EC2 instances to spend their processing power on application tasks, which helps improve overall performance.

-   Elastic Load Balancers (along with CloudFront) support Perfect Forward Secrecy. This is a feature that provides additional safeguards against the eavesdropping of encrypted data in transit through the use of a uniquely random session key. This is done by ensuring that the in-use part of an encryption system automatically and frequently changes the keys it uses to encrypt and decrypt information. So if this latest key is compromised at all, it will only expose a small portion of the user's recent data.

-   Classic Load Balancers do not support Server Name Indication (SNI). SNI allows the server (the LB in this case) to safely host multiple TLS Certificates for multiple sites all under a single IP address (the Alias record or CName record in this case). To allow SNI, you have to use an Application Load Balancer instead or use it with a CloudFront web distribution.

---

# CloudWatch

Amazon CloudWatch is a monitoring and observability service. It provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health.

![alt text](/Photos/image27.png)

-   CloudWatch collects monitoring and operational data in the form of logs, metrics, and events.
-   You can use CloudWatch to detect anomalous behavior in your environments, set alarms, visualize logs and metrics side by side, take automated actions, troubleshoot issues, and discover insights to keep your applications running smoothly.
-   Within the compute domain, CloudWatch can inform you about the health of EC2 instances, Autoscaling Groups, Elastic Load Balancers, and Route53 Health Checks. Within the storage and content delivery domains, CloudWatch can inform you about the health of EBS Volumes, Storage Gateways, and CloudFront.
-   With regards to EC2, CloudWatch can only monitor host level metrics such as CPU, network, disk, and status checks for insights like the health of the underlying hypervisor.
-   CloudWatch is NOT CloudTrail so it is important to know that only CloudTrail can monitor AWS access for security and auditing reasons. CloudWatch is all about performance. CloudTrail is all about auditing.
-   CloudWatch with EC2 will monitor events every 5 minutes by default, but you can have 1 minute intervals if you use Detailed Monitoring.
-   You can customize your CloudWatch dashboards for insights.
-   There is a multi-platform CloudWatch agent which can be installed on both Linux and Windows-based instances. This agent enables you to select the metrics to be collected, including sub-resource metrics such as per-CPU core. You can use this single agent to collect both system metrics and log files from Amazon EC2 instances and on-premises servers.

-   _The following metrics are not collected from EC2 instances via CloudWatch:_
    -   Memory utilization
    -   Disk swap utilization
    -   Disk space utilization
    -   Page file utilization
    -   Log collection
-   **If you need information, then you can retrieve it via the official CloudWatch agent or you can create a custom metric and send the data on your own via a custom script.**

-   _CloudWatch's key purpose:_
    -   Collect metrics
    -   Collect logs
    -   Collect events
    -   Create alarms
    -   Create dashboards

## CloudWatch Logs:

-   You can use Amazon CloudWatch Logs to monitor, store, and access your log files from Amazon EC2 instances, AWS CloudTrail, Amazon Route 53, and other sources. You can then retrieve the associated log data from CloudWatch Logs.
-   It helps you centralize the logs from all of your systems, applications, and AWS services that you use, in a single, highly scalable service.
-   You can create log groups so that you join logical units of CloudWatch Logs together.
-   You can stream custom log files for further insights.

## Log Stream :

A collection of log events from the same source creates a log stream. Think of one continuous set of logs from a single instance.

## Log Group :

This is a collection of log streams. For example, you would group all your Apache web server logs across hosts together.

## CloudWatch Events:

-   Amazon CloudWatch Events delivers a near real-time stream of system events that describe changes in AWS resources.

-   You can use events to trigger lambdas for example while using alarms to inform you that something went wrong.

## CloudWatch Alarms:

-   CloudWatch alarms send notifications or automatically make changes to the resources you are monitoring based on rules that you define.
-   For example, you can create custom CloudWatch alarms which will trigger notifications such as surpassing a set billing threshold.
-   CloudWatch alarms have two states of either `ok` or `alarm`.

## CloudWatch Metrics:

-   CloudWatch Metrics represent a time-ordered set of data points.
-   These basically are a variable you can monitor over time to help tell if everything is okay, e.g. Hourly CPU Utilization.
-   CloudWatch Metrics allows you to track high resolution metrics at sub-minute intervals all the way down to per second.

## CloudWatch Dashboards:

-   CloudWatch dashboards are customizable home pages in the CloudWatch console that you can use to monitor your resources in a single view
-   These dashboards integrate with CloudWatch Metrics and CloudWatch Alarms to create customized views of the metrics and alarms for your AWS resources.

## Amazon Managed Grafana -

Fully managed AWS service allowing secure data visualizations for instantly querying, correlating, and visualizing your operational metrics, logs, and traces from different sources.

![alt text](/Photos/image28.png)

-   Easily deploy, operate, and scale Grafana within your AWS accounts.
-   Built-in security features help you meet corporate governance and compliance requirements.
-   Workspaces (logical Grafana servers) allow for separation of data visualizations and querying.
-   Pricing is based per active user in a workspace.
-   AWS handles scaling, setup, and maintenance of all workspaces.
-   Integrate it with several sources including Amazon CloudWatch, Amazon Managed Service for Prometheus, Amazon OpenSearch Service, and Amazon Timestream.

### Use Cases :

-   Connect to data sources like Prometheus for visualizing EKS, ECS, or your own Kubernetes cluster metrics.
-   Vast data plugins make the service a perfect fit for monitoring loT and edge device data.
-   Centralizing dashboards allows for more efficient operational issue troubleshooting.

## Amazon Managed Service for Prometheus -

![alt text](/Photos/image29.png)

Serverless, Prometheus-compatible service used for securely monitoring container metrics at scale

-   Leverage the open-source Prometheus data model with AWS-managed scaling and availability.
-   Let AWS manage automatic scaling based on ingestion, storage,
-   AWS replicates data across three
    Availability Zones (AZs) in the same Region. Designed for availability.

-   Works with clusters running on Amazon
    EKS or self-managed Kubernetes clusters.
-   Leverage the open-source PromQL query language for exploring and extracting data.
-   Data is stored in workspaces for 150 days (automatically deleted afterward).

---

# Scaling

## What Is Horizontal Scaling?

Horizontal scaling (aka scaling out) refers to adding additional nodes or machines to your infrastructure to cope with new demands. If you are hosting an application on a server and find that it no longer has the capacity or capabilities to handle traffic, adding a server may be your solution.

![alt text](/Photos/image32.png)

## What Is Vertical Scaling?

Vertical scaling (aka scaling up) describes adding additional resources to a system so that it meets demand.

While horizontal scaling refers to adding additional nodes, vertical scaling describes adding more power to your current machines. For instance, if your server requires more processing power, vertical scaling would mean upgrading the CPUs. You can also vertically scale the memory, storage, or network speed.

![alt text](/Photos/image33.png)

![alt text](/Photos/image30.png)

## Launch Template :

A launch template specifies all the needed settings that go into building out an EC2 instance. It is a collection of settings you can configure so you don't have to walk through the EC2 wizard over and over.

It includes the AMI, EC2 instance size, security groups, and potentially networking information.

_Baking your code into your AMIs will help reduce provisioning time._

![alt text](/Photos/image31.png)

-   The most up-to-date and flexible way to create a template.
-   The older version. It's not
    "wrong" to use them, but, if possible, use templates.
-   User data is included in the template or configuration.
-   Can be versioned. Configurations are immutable.
-   Configurations don't include networking information. Templates could.

---

# Auto Scaling :

AWS Auto Scaling lets you build scaling plans that automate how groups of different resources respond to changes in demand. You can optimize availability, costs, or a balance of both. AWS Auto Scaling automatically creates all of the scaling policies and sets targets for you based on your preference.

> Auto Scaling is only for EC2. No other service can be scaled using Auto Scaling. Other services might have a built-in option, but they aren't included in Auto Scaling groups.

When you use Elastic Load Balancing with your Auto Scaling group, it's not necessary to register individual EC2 instances with the load balancer. Instances that are launched by your Auto Scaling group are automatically registered with the load balancer. Likewise, instances that are terminated by your Auto Scaling group are automatically deregistered from the load balancer

_Auto Scaling Steps :_
![alt text](/Photos/image34.png)

### Lifecylcle Hooks :

As your Auto Scaling group scale-out or scale-in your EC2 instances, you may want to perform custom actions before they start accepting traffic or before they get terminated. Auto Scaling Lifecycle Hooks allow you to perform custom actions during these stages.

For example, during the scale-out event of your ASG(Auto Scaling Group), you want to make sure that new EC2 instances download the latest code base from the repository and that your EC2 user data has completed before it starts accepting traffic. This way, the new instances will be fully ready and will quickly pass the load balancer health check when they are added as targets. Another example is this – during the scale-in event of you ASG, suppose your instances upload data logs to S3 every minute. You may want to pause the instance termination for a certain amount of time to allow the EC2 to upload all data logs before it gets completely terminated.

![alt text](/Photos/image35.png)

**STEPS :**

1. EC2 instance gets launched by EC2 Auto Scaling group
2. WAIT state is entered via the Lifecycle Hooks capability
3. While in the WAIT state, the instance runs a custom script via EC2 user data to install a proprietary application
4. Script install and configure application
5. Once the application is validated to be working correctly, the instance sends a complete-lifecycle-action command

### Auto Scaling Policies :

1. **Step Scaling** : To use step scaling, you first create a CloudWatch alarm that monitors a metric for your Auto Scaling group. Define the metric, threshold value, and number of evaluation periods that determine an alarm breach. Then, create a step scaling policy that defines how to scale your group when the alarm threshold is breached.

![alt text](/Photos/image36.png)

![alt text](/Photos/image37.png)

2. **Simple Scaling** : Simple scaling relies on a metric as a basis for scaling. For example, you can set a CloudWatch alarm to have a CPU Utilization threshold of 80%, and then set the scaling policy to add 20% more capacity to your Auto Scaling group by launching new instances. Accordingly, you can also set a CloudWatch alarm to have a CPU utilization threshold of 30%. When the threshold is met, the Auto Scaling group will remove 20% of its capacity by terminating EC2 instances.

3. **Target Tracking** : Target tracking policy lets you specify a scaling metric and metric value that your auto scaling group should maintain at all times. Let’s say for example your scaling metric is the average CPU utilization of your EC2 auto scaling instances, and that their average should always be 80%. When CloudWatch detects that the average CPU utilization is beyond 80%, it will trigger your target tracking policy to scale out the auto scaling group to meet this target utilization. Once everything is settled and the average CPU utilization has gone below 80%, another scale in action will kick in and reduce the number of auto scaling instances in your auto scaling group. With target tracking policies, your auto scaling group will always be running in a capacity that is defined by your scaling metric and metric value.

**Instance Warm-Up and Cooldown** -

-   _Warm-Up_ :
    Stops instances from being placed behind the load balancer, failing the health check, and being terminated prematurely.
-   _Cooldown_ :
    Pauses Auto Scaling for a set amount of time.
    Helps to avoid runaway scaling events.
-   _Avoid Thrashing_ :
    You want to create instances quickly and spin them down slowly.

_Scaling Types :-_

![alt text](/Photos/image38.png)

## Scaling Non-Relational Databases

_Types of Scaling -_

There are 4 types of scaling we can use to adjust our relational database performance.

![alt text](/Photos/image39.png)

_Scaling Options -_
Scaling is simplified when using DynamoDB, as AWS does all the heavy lifting for you.

![alt text](/Photos/image40.png)

**Capacity Units :**

### Read Capacity Unit (RCU)

DynamoDB unit of measurement for reads per second for an item up to 4 KB in size.

One strongly consistent read per second.

Two eventually consistent reads per second.

_Knowledge Check: How many RCUs for 1 strongly consistent read per second for objects that are 7 KB in size?_

1 RCU = 4 KB / 1 Strongly Consistent Read.

Round up to the next nearest amount for the item size = 8 KB / 4 KB = 2 RCU

### Write Capacity Unit (WCU)

DynamoDB unit of measurement for writes per second for an item up to 1 KB in size.

Knowledge Check: How many WCUs for 1 write per second for an object that is 3 KB in size?

1 WCU = 1 KB \* 1 Write per Second

3 KB \* 1 WCU = 3 WCUs

**Non-Relational Database Scaling** -

-   Access Patterns :
    Know if your access patterns are predicable or unpredictable.
-   Design Matters :
    Avoiding hot keys will also lead to better performance.

-   Switching :
    You can switch, but only twice per 24 hours per table.

-   Cost :
    Keep cost in mind when considering which type of table to pick.

## Different Disaster Recovery Strategies

-   **Recovery Point Objective (RPO)** :
    In the event of a disaster/failure, at what point in time do you want your data recovered to? Put simply, how much data can you afford to lose?
    Twenty-four hours? Twelve hours?
    Minutes? Seconds?

    Typically speaking, the lower the time, the greater the cost.

-   **Recovery Time Objective (RTO)** :
    In the event of a failure, how fast do you want to fail over? How much time can the business afford? The lower the time, the more expensive the cost.

-   **Backup and Restore** :
    The simplest disaster recovery strategy. If something happens to your production system, restore that system from backup.

-   **Pilot Light** :
    A pilot light in a home hot water system is where a small light burns so that when you want to turn the hot water system on, it starts straight away. When a pilot light is burning, it is not consuming the same level of gas as when the system is on.
    ![alt text](/Photos/image41.png)

-   **Warm Standby** :
    Where you have a scaled-down version of your production system already running in another Availability Zone/Region. You then scale this system up in the event of an outage.

-   **Active/ Active Failover** :
    The most expensive disaster recovery strategy. You have two sites, both active and traffic split between the two. If one site fails, the other site takes the load. Generally, you have to have both sites at 200% normal capacity to avoid downtime.

### Auto Scaling Cooldown Period:

The cooldown period is a configurable setting for your Auto Scaling Group that helps to ensure that it doesn't launch or terminate additional instances before the previous scaling activity takes effect.

After the Auto Scaling Group scales using a policy, it waits for the cooldown period to complete before resuming further scaling activities if needed.

The default waiting period is 300 seconds, but this can be modified.

---

# Decoupling Workflows

**Loose Coupling -**

![alt text](/Photos/image42.png)

**Tight Coupling -**

![alt text](/Photos/image43.png)

_Poll-based messaging is a request/response approach where a client sends a message to a server and waits for a response._

---

# Simple Queuing Service (SQS)

SQS is a web-based service that gives you access to a message queue that can be used to store messages while waiting for another service to process them. It helps in the decoupling of systems and the horizontal scaling of AWS resources.

Simple Queue Service is a messaging queue that allows asynchronous processing of work. One resource will write a message to an SQS queue, and then another resource will retrieve that message from SQS.

The point behind SQS is to decouple work across systems. This way, downstream services in a system can perform work when they are ready to rather than when upstream services feed them data.

> In a hypothetical AWS environment running without SQS, Application A would pass Application B data regardless if Application B was ready to receive the info. With SQS however, there is an intermediary step where the data is stored temporarily in a buffer. It waits there until Application B pulls the temporarily stored data. SQS is not a push-based service so it is necessary for SQS to work in tandem with another service that queries it for information.

There are two types of SQS queues; standard and FIFO. Standard queues may be received out of order based on message size or however else the SQS queues decide to optimize. **FIFO queues** guarantees that the order of messages that went into the queue is the same as the order of messages that leave it.

**Standard SQS queues** guarantee that a message is delivered at least once and because of this, it is possible on occasion that a message might be delivered more than once due to the asynchronous and highly distributed architecture. With standard queues, you have a nearly unlimited number of transactions per second.

-   FIFO SQS queues guarantee exactly-once processing and is limited to 300 transactions per second.
-   Messages in the queue can be kept there from one minute to 14 days and the default retention period is 4 days.

-   An SQS queue can contain an unlimited number of messages.
-   You cannot set a priority to the individual items in the SQS queue. If priority of messaging matters, create two separate SQS queues. The SQS queues for the priority message can be polled first by the EC2 Instances and once completed, the messages from the second queue can be processed next.

### Amazon SQS visibility timeout

Visibility timeouts in SQS are the mechanism in which messages marked for delivery from the queue are given a time frame to be fully received by a reader. This is done by temporarily making them invisible to other readers. If the message is not fully processed within the time limit, the message becomes visible again. This is another way in which messages can be duplicated. If you want to reduce the chance of duplication, increase the visibility timeout.

The visibility timeout maximum is 12 hours.

Always remember that the messages in the SQS queue will continue to exist even after the EC2 instance has processed it, until you delete that message. You have to ensure that you delete the message after processing to prevent the message from being received and processed again once the visibility timeout expires.

![alt text](/Photos/image44.png)

### SQS Polling:

-   Polling is the means in which you query SQS for messages or work. Amazon SQS provides short-polling and long-polling to receive messages from a queue. By default, queues use short polling.
-   **SQS long-polling** : This polling technique will only return from the queue once a message is there, regardless if the queue is currently full or empty. This way, the reader needs to wait either for the timeout set or for a message to finally arrive. SQS long polling doesn't return a response until a message arrives in the queue, reducing your overall cost over time.
-   **SQS short-polling** : This polling technique will return immediately with either a message that’s already stored in the queue or empty-handed.
-   The ReceiveMessageWaitTimeSeconds is the queue attribute that determines whether you are using Short or Long polling. By default, its value is zero which means it is using short-polling. If it is set to a value greater than zero, then it is long-polling.
-   Every time you poll the queue, you incur a charge. So thoughtfully deciding on a polling strategy that fits your use case is important.

### Dead-Letter Queues :

-   Amazon SQS Dead-letter queues (DLQ) are targets for messages that cannot be processed successfully.
-   Works with SQS and SNS!
-   Useful for debugging applications and messaging systems.
-   Ability to isolate unconsumed messages to troubleshoot.
-   Redrive capability allows you to move the message back into the source queue!
-   These are technically just other SQS queues!
-   DLQs used with FIFO SQS queues must ALSO be FIFO queues.

**Dead-Letter Queues Benefits** -

-   Configure alarms based on message availability counts.
-   Quickly identify which logs to investigate for exceptions.
-   Analyze the SQS message contents for any errors.
-   Troubleshoot consumer permissions.

![alt text](/Photos/image45.png)

---

**What is push-based messaging?**

Any messages sent by a producer that arrives at the SNS Topic will immediately be sent to all consumers.

# Simple Notification Service (SNS)

Simple Notification Service is a pushed-based messaging service that provides a highly scalable, flexible, and cost-effective method to publish a custom messages to subscribers who wish to be informed about a certain topic.

-   This can be used to alert a system or a person.

-   One message to many receivers!

-   SNS is mainly used to send alarms or alerts.
-   SNS provides topics for high-throughput, push-based, many-to-many messaging.
-   Using Amazon SNS topics, your publisher systems can fan out messages to a large number of subscriber endpoints for parallel processing, including Amazon SQS queues, AWS Lambda functions, and HTTP/S webhooks. Additionally, SNS can be used to fan out notifications to end users using mobile push, SMS, and email.
-   You can send these push notifications to Apple, Google, Fire OS, and Windows devices.
-   SNS allows you to group multiple recipients using topics. A topic is an access point for allowing recipients to dynamically subscribe for identical copies of the same notification.
-   One topic can support deliveries to multiple endpoint types. When you publish to a topic, SNS appropriately formats copies of that message to send to whichever kind of device.
-   To prevent messages being lost, messages are stored redundantly across multiple AZs.
-   There is no long or short polling involved with SNS due to the instantaneous pushing of messages
-   SNS has flexible message delivery over multiple transport protocols and has a simple API.

> -   Messages can be up to 256 KB of text in any format.
> -   Messages that fail to be delivered can be stored in an SQS DLQ.
> -   FIFO only supports SQS FIFO queues as a subscriber.
> -   Messages are encrypted in transit by default, and you can add at-rest via AWS KMS.
> -   A resource policy can be added to a topic, similar to S3. Useful for cross-account access.

-   The SNS Extended Library allows for sending messages up to 2 GB in size.
    The payload is stored in Amazon S3, then
    SNS publishes a reference to the object.

> -   **By default, every message published to a topic is sent to all subscribers**
>
> -   **Filter policies use JSON to define which messages get sent to specific subscribers**

![alt text](/Photos/image46.png)

---

# API Gateway

API Gateway is a fully managed service for developers that makes it easy to build, publish, manage, and secure entire APIs. With a few clicks in the AWS Management Console, you can create an API that acts as a “front door” for applications to access data, business logic, or functionality from your back-end services, such as workloads running on EC2, code running on AWS Lambda, or any web application.

Amazon API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, authorization and access control, monitoring, and API version management.

Amazon API Gateway has no minimum fees or startup costs. You pay only for the API calls you receive and the amount of data transferred out.

_API Gateway does the following for your APIs:_

-   Exposes HTTP(S) endpoints for RESTful functionality
-   Uses serverless functionality to connect to Lambda & DynamoDB
-   Can send each API endpoint to a different target
-   Runs cheaply and efficiently
-   Scales readily and effortlessly
-   Can throttle requests to prevent attacks
-   Track and control usage via an API key
-   Can be version controlled
-   Can be connected to CloudWatch for monitoring and observability

Since API Gateway can function with AWS Lambda, you can run your APIs and code without needing to maintain servers.

Amazon API Gateway provides throttling at multiple levels including global and by a service call.

-   In software, a throttling process, or a throttling controller as it is sometimes called, is a process responsible for regulating the rate at which application processing is conducted, either statically or dynamically.
-   Throttling limits can be set for standard rates and bursts. For example, API owners can set a rate limit of 1,000 requests per second for a specific method in their REST APIs, and also configure Amazon API Gateway to handle a burst of 2,000 requests per second for a few seconds.
-   Amazon API Gateway tracks the number of requests per second. Any requests over the limit will receive a 429 HTTP response. The client SDKs generated by Amazon API Gateway retry calls automatically when met with this response.

You can add caching to API calls by provisioning an Amazon API Gateway cache and specifying its size in gigabytes. The cache is provisioned for a specific stage of your APIs. This improves performance and reduces the traffic sent to your back end. Cache settings allow you to control the way the cache key is built and the time-to-live (TTL) of the data stored for each method. Amazon API Gateway also exposes management APIs that help you invalidate the cache for each stage.

You can enable API caching for improving latency and reducing I/O for your endpoint.

When caching for a particular API stage (version controlled version), you cache responses for a particular TTL in seconds.

API Gateway supports AWS Certificate Manager and can make use of free TLS/SSL certificates.

With API Gateway, there are two kinds of API calls:

-   Calls to the API Gateway API to create, modify, delete, or deploy REST APIs. These are logged in CloudTrail.
-   API calls set up by the developers to deliver their custom functionality: These are not logged in CloudTrail.

**API Options :**

![alt text](/Photos/image47.png)

_Endpoint Types :_

-   Edge-Optimized : Default option. API requests get sent through a CloudFront edge location. Best for global users.
-   Regional : Perfect for clients that reside in the same, specific region.
    Ability to also leverage with CloudFront if required.
-   Private : Only accessible via VPCs using interface VPC endpoints.

# AWS Batch

Batch computing run jobs asynchronously and automatically across multiple compute instances. While running a single job may be trivial, running many at scale, particularly with multiple dependencies, can be more challenging. This is where using a fully managed service such as AWS Batch offers significant benefit.

_Solutions built on AWS Batch allow developers to build efficient, long-running compute jobs by focusing on the business logic required, while AWS manages the scheduling and provisioning of the work._

As a fully managed service, AWS Batch helps you to run batch computing workloads of any scale. AWS Batch automatically provisions compute resources and optimizes the workload distribution based on the quantity and scale of the workloads. With AWS Batch, there's no need to install or manage batch computing software, so you can focus your time on analyzing results and solving problems.

**Batch Components :**

-   Jobs — the unit of work submitted to AWS Batch, whether it be implemented as a shell script, executable, or Docker container image.
-   Job Definition — describes how your work is be executed, including the CPU and memory requirements and IAM role that provides access to other AWS services.
-   Job Queues — listing of work to be completed by your Jobs. You can leverage multiple queues with different priority levels.
-   Compute Environment — the compute resources that run your Jobs. Environments can be configured to be managed by AWS or on your own as well as the number of and type(s) of instances on which Jobs will run. You can also allow AWS to select the right instance type.

**Fargate VS EC2** -

![alt text](/Photos/image48.png)

**AWS Batch VS AWS Lambda** -

![alt text](/Photos/image49.png)

**Managed vs Unmanaged Compute Environment :**

![alt text](/Photos/image50.png)

# Amazon MQ

-   Amazon MQ is a managed message broker service that makes it easy to set up and operate message brokers in the cloud.
-   The service is used when migrating services and apps into the cloud from your on-prem which is how it differs from Amazon SQS.
-   Amazon MQ supports durability-optimized brokers backed by Amazon EFS to support high availability and message durability, and throughput-optimized brokers backed by Amazon EBS to support high-volume applications that require low latency and high throughput.
-   You can easily move from any message broker to Amazon MQ because you don’t have to rewrite any messaging code in your applications.
-   Amazon MQ is suitable for enterprise IT pros, developers, and architects who are managing a message broker themselves–whether on-premises or in the cloud–and want to move to a fully managed cloud service without rewriting the messaging code in their applications.
-   Currently supports both Apache ActiveMQ or RabbitMQ engine types

**Amazon MQ Brokers :**
![alt text](/Photos/image51.png)

# AWS Step Functions

AWS Step Functions is a serverless orchestration service that lets you integrate with AWS Lambda functions and other AWS services to build business-critical applications. Through Step Functions' graphical console, you see your application’s workflow as a series of event-driven steps.

Step Functions is based on state machines and tasks. In Step Functions, a workflow is called a state machine, which is a series of event-driven steps. Each step in a workflow is called a state. A Task state represents a unit of work that another AWS service, such as AWS Lambda, performs. A Task state can call any AWS service or API.

With Step Functions' built-in controls, you examine the state of each step in your workflow to make sure that your application runs in order and as expected. Depending on your use case, you can have Step Functions call AWS services, such as Lambda, to perform tasks. You can create workflows that process and publish machine learning models. You can have Step Functions control AWS services, such as AWS Glue, to create extract, transform, and load (ETL) workflows. You also can create long-running, automated workflows for applications that require human interaction.

> All state machines are written in the Amazon States Language format.

**Execution Types -**

![alt text](/Photos/image52.png)

_Different States :_

-   `Pass` : Passes any input directly to its output (no work done)
-   `Task` : Single unit of work performed (e.g., Lambda, Batch, and SNS)
-   `Choice` : Adds branching logic to state machines
-   `Wait` : Creates a specified time delay within the state machine
-   `Succeed` : Stops executions successfully
-   `Fail` : Stops executions and marks them as failures
-   `Parallel` : Runs parallel branches of executions within state machines
-   `Map` : Runs a set of steps based on elements of an input array

# Amazon AppFlow

Amazon AppFlow is a fully-managed integration service that enables you to securely exchange data between software as a service (SaaS) applications, such as Salesforce, and AWS services, such as Amazon Simple Storage Service (Amazon S3) and Amazon Redshift. For example, you can ingest contact records from Salesforce to Amazon Redshift or pull support tickets from Zendesk to an Amazon S3 bucket.

![alt text](/Photos/image53.png)

**BENEFITS** -

-   _Speed and agility_
-   _Privacy and security_
-   _Scalability_
-   _Reliability_

_AppFlow Use Cases_ -

-   Transferring Salesforce records to Amazon Redshift
-   Ingesting and analyzing Slack conversations in S3
-   Migrating Zendesk and other help desk support tickets to Snowflake
-   Transferring aggregate data on a scheduled basis to S3\*

> \*Up to 100 GB per flow

# BIG DATA

3 Vs that differentiate big data from traditional data -

-   Volume : Ranges from terabytes to petabytes of data.
-   Variety : Includes data from a wide range of sources and formats.
-   Velocity : Data needs to be collected, stored, processed, and analyzed within a short period of time.

---

# Amazon Redshift

Amazon Redshift is a fully managed, petabyte-scale data warehouse service in the cloud. The Amazon Redshift service manages all of the work of setting up, operating, and scaling a data warehouse. These tasks include provisioning capacity, monitoring and backing up the cluster, and applying patches and upgrades to the Amazon Redshift engine.

-   Redshift is incredibly big — it can hold up to 16 PB of data. You don't have to split up your large datasets!

-   This database is relational. You use your standard SQL and business intelligence (BI) tools to interact with it.

-   This is based on the PostgreSQL database engine type; however, it is NOT used for OLTP workloads!

-   Redshift is not meant to be a replacement for standard RDS databases.

-   Offers up to 10x the performance of other data warehouses offered in the cloud!

-   Storage of data is column-based instead of row-based. Allows for efficient parallel queries.

-   Redshift now supports Multi-AZ deployments! It only spans two AZs at this time.

-   Snapshots are incremental and point-in-time. They can be automated or manual.
    Always contained in Amazon S3 (you cannot manage the bucket).
-   No conversions from Single-AZ to Multi-AZ (or vice versa)!

Redshift is used for business intelligence and pulls in very large and complex datasets to perform complex queries in order to gather insights from the data.
It fits the use case of Online Analytical Processing (OLAP). Redshift is a powerful technology for data discovery including capabilities for almost limitless report viewing, complex analytical calculations, and predictive “what if” scenario (budget, forecast, etc.) planning.

Redshift can also asynchronously replicate your snapshots to a different region if desired.

Redshift is encrypted in transit using SSL and is encrypted at rest using AES-256. By default, Redshift will manage all keys, but you can do so too via AWS CloudHSM or AWS KMS.

Redshift is billed for:

-   Compute Node Hours (total hours your non-leader nodes spent querying for data)
-   Backups
-   Data transfer within a VPC (but not outside of it)

### Redshift Spectrum -

-   Efficiently query and retrieve data from Amazon S3 without having to load the data into Amazon
    Redshift tables.

-   Massive parallelism allows this to run very fast against large datasets. Uses Redshift servers that are independent of your cluster!

-   The cluster and the data files in Amazon S3 must be in the same AWS Region.
-   External S3 tables are read-only. You can't perform insert, update, or delete operations on external tables.

### Enhanced VPC Routing -

-   When you use Amazon Redshift Enhanced VPC Routing, Redshift forces all traffic (such as COPY and UNLOAD traffic) between your cluster and your data repositories through your Amazon VPC.
-   If Enhanced VPC Routing is not enabled, Amazon Redshift routes traffic through the Internet, including traffic to other services within the AWS network.
-   By using Enhanced VPC Routing, you can use standard VPC features, such as VPC security groups, network access control lists (ACLs), VPC endpoints, VPC endpoint policies, internet gateways, and Domain Name System (DNS) servers.

## ETL

ETL stands for Extract, Transform, Load. It's a process used in data warehousing and data integration to gather data from various sources, transform it into a consistent format, and load it into a target database or data warehouse.

ETL processes are crucial in ensuring that data is effectively collected, integrated, and made available for analysis and decision-making purposes within organizations. They help maintain data quality, consistency, and integrity across disparate data sources.

# EMR

Amazon EMR (previously called Amazon Elastic MapReduce) is a managed cluster platform that simplifies running big data frameworks, such as Apache Hadoop and Apache Spark, on AWS to process and analyze vast amounts of data. Using these frameworks and related open-source projects, you can process data for analytics purposes and business intelligence workloads. Amazon EMR also lets you transform and move large amounts of data into and out of other AWS data stores and databases, such as Amazon Simple Storage Service (Amazon S3) and Amazon DynamoDB.

**EMR Storage** -

-   Hadoop Distributed File System (HDFS) :
    Distributed, scalable file system for Hadoop that distributes stored data across instances. Used for caching results during processing.

-   EMR File System (EMRFS) :
    Extends Hadoop to add the ability to directly access data stored in Amazon S3 as if it were a part of HDFS. S3 is typically used to store input and output data, not intermediate data.
-   Local file system :
    Locally connected disk created with each EC2 instance. Instance store volumes only remain during the lifecycle of the Amazon EC2 instance.

_Amazon EMR Clusters and Nodes :_
Clusters are groups of EC2 instances within Amazon EMR. Each instance is a node.

Primary Node :
Manages the cluster, coordinates distribution of data and tasks, tracks health statuses.

Core Node :
Runs tasks and stores data in Hadoop Distributed File System (HDFS). Long-running!

Task Node :
ONLY runs tasks, with no storage of data within HDFS. Optional. Typically Spot instances.

_Purchasing Options and Cluster Types :_

-   On-Demand :
    Most reliable purchase option. Will not be terminated. Most expensive choice.

-   Reserved : Just like other reserved instances.
    Minimum of 1 year. Offers great cost savings. Typically used for primary nodes and core nodes.
-   Spot :
    Cheapest option available. Can be terminated with little warning. Typically used for task nodes.
-   Long-Running or Temporary :
    Clusters can be either long-running, or they can be transient (a.k.a. temporary).

![alt text](/Photos/image55.png)

> Toolsets to Keep in Mind -
>
> Built-in support for Spark, Hive, HBase, Flink, Hudi, and Presto.

---

# Kinesis

Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information. With Amazon Kinesis, you can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications. Amazon Kinesis enables you to process and analyze data as it arrives and respond instantly instead of having to wait until all your data is collected before the processing can begin.

Amazon Kinesis makes it easy to load and analyze the large volumes of data entering AWS.

Kinesis is used for processing real-time data streams (data that is generated continuously) from devices constantly sending data into AWS so that said data can be collected and analyzed.

It is a fully managed service that automatically scales to match the throughput of your data and requires no ongoing administration. It can also batch, compress, and encrypt the data before loading it, minimizing the amount of storage used at the destination and increasing security.

_There are three different types of Kinesis:_

-   **Kinesis Streams** - Kinesis Streams works where the data producers stream their data into Kinesis Streams which can retain the data from one day up until 7 days. Once inside Kinesis Streams, the data is contained within shards.
    Kinesis Streams can continuously capture and store terabytes of data per hour from hundreds of thousands of sources such as website clickstreams, financial transactions, social media feeds, IT logs, and location-tracking events. For example: purchase requests from a large online store like Amazon, stock prices, Netflix content, Twitch content, online gaming data, Uber positioning and directions, etc.

![alt text](/Photos/image56.png)

-   **Kinesis Firehose** : Amazon Kinesis Firehose is the easiest way to load streaming data into data stores and analytics tools. When data is streamed into Kinesis Firehose, there is no persistent storage there to hold onto it. The data has to be analyzed as it comes in so it's optional to have Lambda functions inside your Kinesis Firehose. Once processed, you send the data elsewhere.
    Kinesis Firehose can capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk, enabling near real-time analytics with existing business intelligence tools and dashboards you’re already using today.

    > Kinesis Firehose is auto scalable.

![alt text](/Photos/image57.png)

-   **Kinesis Analytics** : Kinesis Analytics works with both Kinesis Streams and Kinesis Firehose and can analyze data on the fly. The data within Kinesis Analytics also gets sent elsewhere once it is finished processing. It analyzes your data inside of the Kinesis service itself. The data can even be transformed.

> **Kinesis vs. SQS**
>
> ![alt text](/Photos/image58.png)

---

# Amazon Athena

AWS Athena is an interactive query service that makes it easy to analyze data directly in Amazon Simple Storage Service (Amazon S3) using standard SQL. It's a serverless service, meaning there's no infrastructure to manage, and you only pay for the queries you run.

# Amazon Glue

AWS Glue is a serverless data integration service that makes it easy for analytics users to discover, prepare, move, and integrate data from multiple sources. You can use it for analytics, machine learning, and application development. It also includes additional productivity and data ops tooling for authoring, running jobs, and implementing business workflows.

With AWS Glue, you can discover and connect to more than 70 diverse data sources and manage your data in a centralized data catalog. You can visually create, run, and monitor extract, transform, and load (ETL) pipelines to load data into your data lakes.

---

# Amazon QuickSight

Amazon QuickSight is a cloud-scale business intelligence (BI) service that you can use to deliver easy-to-understand insights to the people who you work with, wherever they are. Amazon QuickSight connects to your data in the cloud and combines data from many different sources. In a single data dashboard, QuickSight can include AWS data, third-party data, big data, spreadsheet data, SaaS data, B2B data, and more.

-   Users can be created for accessing
    QuickSight
-   Enterprise version allows you to also create groups
-   Users and groups only exist in QuickSight
-   Dashboards allow for stored configurations and filtering
-   You can share dashboards and analysis results with users and groups

---

# AWS Data Pipeline

AWS CodePipeline is a continuous delivery service you can use to model, visualize, and automate the steps required to release your software. You can quickly model and configure the different stages of a software release process. CodePipeline automates the steps required to release your software changes continuously.

# Amazon MSK

Amazon Managed Streaming for Apache Kafka (Amazon MSK) is a fully managed service that enables you to build and run applications that use Apache Kafka to process streaming data. Amazon MSK provides the control-plane operations, such as those for creating, updating, and deleting clusters. It lets you use Apache Kafka data-plane operations, such as those for producing and consuming data. It runs open-source versions of Apache Kafka. This means existing applications, tooling, and plugins from partners and the Apache Kafka community are supported without requiring changes to application code.

-   Broker nodes — When creating an Amazon MSK cluster, you specify how many broker nodes you want Amazon MSK to create in each Availability Zone. In the example cluster shown in this diagram, there's one broker per Availability Zone. Each Availability Zone has its own virtual private cloud (VPC) subnet.

-   ZooKeeper nodes — Amazon MSK also creates the Apache ZooKeeper nodes for you. Apache ZooKeeper is an open-source server that enables highly reliable distributed coordination.

-   Producers, consumers, and topic creators — Amazon MSK lets you use Apache Kafka data-plane operations to create topics and to produce and consume data.

-   Cluster Operations You can use the AWS Management Console, the AWS Command Line Interface (AWS CLI), or the APIs in the SDK to perform control-plane operations. For example, you can create or delete an Amazon MSK cluster, list all the clusters in an account, view the properties of a cluster, and update the number and type of brokers in a cluster.

Amazon MSK detects and automatically recovers from the most common failure scenarios for clusters so that your producer and consumer applications can continue their write and read operations with minimal impact. When Amazon MSK detects a broker failure, it mitigates the failure or replaces the unhealthy or unreachable broker with a new one. In addition, where possible, it reuses the storage from the older broker to reduce the data that Apache Kafka needs to replicate. Your availability impact is limited to the time required for Amazon MSK to complete the detection and recovery. After a recovery, your producer and consumer apps can continue to communicate with the same broker IP addresses that they used before the failure.

#### Resiliency in Amazon MSK :

-   Automatic detection and recovery from common failure scenarios. Minimal impact!
-   Detected broker failures result in mitigation or replacement of unhealthy nodes.
-   Tries to reuse storage from older brokers during failures to reduce data needing replication.
-   Impact time is limited to however long it takes Amazon MSK to complete detection and recovery.
-   After successful recovery, producers and consumer apps continue to communicate with the same broker IP as before.

![alt text](/Photos/image59.png)

### Security and Logging -

-   Integration with Amazon KMS for SSE requirements
-   Encryption at rest by default
-   TLS 1.2 for encryption in transit between brokers in clusters
-   Deliver broker logs to Amazon CloudWatch, Amazon S3, and Amazon Kinesis Data Firehose
-   Metrics are gathered and sent to CloudWatch
-   All Amazon MSK API calls are logged to AWS Cloud Trail

# Amazon OpenSearch

OpenSearch is a managed service allowing you to run search and analytics engines for
various use cases.
It is the successor to Amazon
Elasticsearch Service.
