# Theory for _AWS Certified Solutions Architect Associate_

-   [`AWS Well-Architected Framework`](#aws-well-architected-framework)
-   [`IAM`](#identity-access-management)
-   [`S3`](#simple-storage-service)
-   [`EC2`](#elastic-compute-cloudec2)
-   [`EBS and EFS`](#elastic-block-storage-and-elastic-file-system)

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

## If you already manage user identities outside of AWS, you can use identity providers instead of creating IAM users in your AWS account. With an identity provider (IdP), you can manage your user identities outside of AWS and give these external user identities permissions to use AWS resources in your account. This is useful if your organization already has its own identity system, such as a corporate user directory. It is also useful if you are creating a mobile app or web application that requires access to AWS resources.

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

![alt text](image.png)

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
-   Enhanced Networking ENI uses single root I/O virtualization to provide high-performance networking capabilities on supported instance types. SR-IOV provides higher I/O and lower throughput and it ensures higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies. SR-IOV does this by dedicating the interface to a single instance and effectively bypassing parts of the Hypervisor which allows for better performance.
-   Adding more ENIs won’t necessarily speed up your network throughput, but Enhanced Networking ENI will.
-   There is no extra charge for using Enhanced Networking ENI and the better network performance it provides. The only downside is that Enhanced Networking ENI is not available on all EC2 instance families and types.
-   You can attach a network interface to an EC2 instance in the following ways:
    -   When it's running (hot attach)
    -   When it's stopped (warm attach)
    -   When the instance is being launched (cold attach).
-   If an EC2 instance fails with ENI properly configured, you (or more likely,the code running on your behalf) can attach the network interface to a hot standby instance. Because ENI interfaces maintain their own private IP addresses, Elastic IP addresses, and MAC address, network traffic will begin to flow to the standby instance as soon as you attach the network interface on the replacement instance. Users will experience a brief loss of connectivity between the time the instance fails and the time that the network interface is attached to the standby instance, but no changes to the VPC route table or your DNS server are required.
-   For instances that work with Machine Learning and High Performance Computing, use EFA (Elastic Fabric Adaptor). EFAs accelerate the work required from the above use cases. EFA provides lower and more consistent latency and higher throughput than the TCP transport traditionally used in cloud-based High Performance Computing systems.
-   EFA can also use OS-bypass (on linux only) that will enable ML and HPC applications to interface with the Elastic Fabric Adaptor directly, rather than be normally routed to it through the OS. This gives it a huge performance increase.
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

>*Note* : By default, the public IP address of an EC2 Instance is released when the instance is stopped even if its stopped temporarily. Therefore, it is best to refer to an instance by its external DNS hostname. If you require a persistent public IP address that can be associated to the same instance, use an Elastic IP address which is basically a static IP address instead.

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
- Amazon EBS provides the ability to create snapshots (backups) of any EBS volume and write a copy of the data in the volume to S3, where it is stored redundantly in multiple Availability Zones

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

>EBS Snapshots are point in time copies of volumes. You can think of Snapshots as photographs of the disk’s current state and the state of everything within it.


### EBS Encryption -

EBS encrypts your volume with a data key using the industry-standard AES-256 algorithm. Amazon EBS encryption uses AWS Key Management Service (AWS KMS) customer master keys (CMK) when creating encrypted volumes and snapshots.

#### What Happens When You Encrypt an EBS Volume?

-   Data at rest is encrypted inside the volume.
-   All data in flight moving between the instance and the volume is encrypted.
-   All snapshots are encrypted.
-   All volumes created from the snapshot are encrypted.

---

Encryption Explored -

-   Handled Transparently :
    Encryption and decryption are handled transparently (you don't need to do anything).
-   Latency :
    Encryption has a minimal
-   Copying :
    Copying an unencrypted snapshot allows encryption.
-   Snapshots :
    Snapshots of encrypted volumes are encrypted.
-   Root Device Volumes :
    You can now encrypt root device volumes upon creation.

#### Steps to Encrypt an Unencrypted Volume :

- Create a snapshot of the unencrypted root device volume.
- Create a copy of the snapshot and select the encrypt option.
- Create an AMI from the encrypted snapshot.
- Use that AMI to launch new encrypted instances.