++++++++++++++++++++++++++++++++++++++++++++

---

# ANALYSIS SERVICES

Amazon Web Services (AWS) offers a comprehensive suite of analytics services to help organizations collect, store, process, analyze, and visualize data. These services cater to a wide range of analytics use cases, from simple data querying to complex machine learning and AI-driven insights.

## Amazon Athena :

Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run.

With Athena, there’s no need for complex extract, transform, and load (ETL) jobs to prepare your data for analysis.

## Amazon EMR :

Amazon EMR, or Amazon Elastic MapReduce, is a cloud-based big data platform provided by Amazon Web Services (AWS). It simplifies the process of processing and analyzing large datasets using popular frameworks like Apache Hadoop, Apache Spark, Apache Hive, Apache HBase, Apache Flink, and Presto. EMR enables you to quickly and cost-effectively launch and scale compute clusters to handle various data processing tasks.

With Amazon EMR, you can run petabyte-scale analysis at less than half of the cost of
traditional on-premises solutions and over 3x faster than standard Apache Spark.

## Amazon Kinesis :

Amazon Kinesis is a platform provided by Amazon Web Services (AWS) for real-time processing of streaming data at scale. It offers a suite of services designed to collect, process, and analyze large streams of data in real-time, enabling businesses to gain insights, take immediate actions, and make data-driven decisions.

-   Amazon Kinesis Data Streams :
    This service allows you to collect and process large streams of data records in real-time.

-   Amazon Kinesis Data Firehose : Data Firehose is a service that simplifies the process of loading streaming data into other AWS services like Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk for near real-time analytics. It automatically scales to match the throughput of your data and requires no ongoing administration.

-   Amazon Managed Service for Apache Flink :
    Amazon Managed Service for Apache Flink is the easiest way to analyze streaming data, gain actionable insights, and respond to your business and customer needs in real time. Amazon Managed Service for Apache Flink reduces the complexity of building, managing, and integrating streaming applications with other AWS services.

    You can detect anomalies, run aggregations, and perform other real-time analytics tasks.

-   Amazon Kinesis Video Streams : This service is designed for capturing, processing, and storing video streams for analytics and machine learning purposes. It can securely stream video from millions of devices worldwide, such as security cameras, dashcams, drones, and other IoT devices.

## Amazon OpenSearch Service :

Amazon OpenSearch Service (OpenSearch Service) makes it easy to deploy, secure, operate, and scale OpenSearch to search, analyze, and visualize data in real-time. With Amazon OpenSearch Service, you get easy-to-use APIs and real-time analytics capabilities to power use-cases such as log analytics, full-text search, application monitoring, and clickstream analytics, with enterprise- grade availability, scalability, and security.

**With OpenSearch you can search any field even partially matches.**

## Amazon Redshift :

Amazon Redshift is the most widely used cloud data warehouse. It makes it fast, simple and cost- effective to analyze all your data using standard SQL and your existing Business Intelligence (BI) tools. It allows you to run complex analytic queries against terabytes to petabytes of structured and semi-structured data, using sophisticated query optimization, columnar storage on high- performance storage, and massively parallel query completion.

## Amazon QuickSight :

Amazon QuickSight is a fast, cloud-powered business intelligence (BI) service that makes it easy for you to deliver insights to everyone in your organization. QuickSight lets you create and publish interactive dashboards that can be accessed from browsers or mobile devices. You can embed dashboards into your applications, providing your customers with powerful self-service analytics. Amazon QuickSight easily scales to tens of thousands of users without any software to install, servers to deploy, or infrastructure to manage.

## AWS Data Exchange :

AWS Data Exchange is a service provided by Amazon Web Services (AWS) that simplifies the process of securely finding, subscribing to, and using third-party data in the cloud. It serves as a marketplace for data, where data providers can publish and sell their data, and data subscribers can easily discover and access the data they need for various use cases.

## AWS Data Pipeline :

AWS Data Pipeline is a web service that helps you reliably process and move data between different AWS compute and storage services, as well as on-premises data sources, at specified intervals.

AWS Data Pipeline helps you easily create complex data processing workloads that are fault tolerant, repeatable, and highly available.

## AWS Glue :

AWS Glue is a fully managed extract, transform, and load (ETL) service provided by Amazon Web Services (AWS). It simplifies the process of building, managing, and running ETL workflows for processing and analyzing data.

## AWS Lake Formation :

AWS Lake Formation is a service provided by Amazon Web Services (AWS) that simplifies the process of setting up, securing, and managing data lakes on AWS. A data lake is a centralized repository that allows you to store structured, semi-structured, and unstructured data at any scale, enabling analytics, machine learning, and other data-driven applications.

## Amazon Managed Streaming for Apache Kafka (Amazon MSK)

Amazon Managed Streaming for Apache Kafka (Amazon MSK) is a fully managed service provided by Amazon Web Services (AWS) for building and running Apache Kafka-based streaming applications. Kafka is an open-source distributed streaming platform used for building real-time data pipelines and streaming applications. Amazon MSK simplifies the setup, management, and operation of Apache Kafka clusters, allowing you to focus on building applications without the overhead of managing infrastructure.

---

# APPLICATION INTEGRATION SERVICES

Amazon Web Services (AWS) offers a range of application integration services that enable seamless communication and interaction between different components of your applications. These services facilitate the building of distributed, loosely coupled systems, which are essential for modern cloud-native architectures.

## AWS Step Functions :

Step Functions is a serverless orchestration service that allows you to coordinate multiple AWS services into serverless workflows. It enables you to design and execute state machines that represent your business processes as a series of steps.

## Amazon AppFlow :

Amazon AppFlow is a fully managed integration service that enables you to securely transfer data between Software-as-a-Service (SaaS) applications such as Salesforce, Zendesk, Slack, and
Application integration 19
Overview of Amazon Web Services AWS Whitepaper ServiceNow, and AWS services such as Amazon S3 and Amazon Redshift, in just a few clicks.

## Amazon EventBridge :

Amazon EventBridge is a serverless event bus service provided by Amazon Web Services (AWS) that makes it easy to connect applications together using events. It allows you to build event-driven architectures and decouple your applications by enabling them to communicate with each other asynchronously through events.

## Amazon MQ :

Amazon MQ is a managed message broker service for Apache ActiveMQ and RabbitMQ that
makes it easy to set up and operate message brokers in the cloud. Message brokers allow different software systems–often using different programming languages, and on different platforms– to communicate and exchange information.

A **message broker** is a middleware component that facilitates communication between different software applications or components by enabling asynchronous message exchange. It acts as an intermediary that receives messages from producers (senders) and delivers them to consumers (receivers) based on certain criteria or rules.

## Amazon Simple Notification Service :

SNS is a fully managed pub/sub messaging service that allows you to fan out messages to multiple recipients. It enables asynchronous message delivery to distributed systems and supports push-based delivery of notifications to a variety of endpoints such as email, SMS, HTTP/S, and more.

## Amazon Simple Queue Service :

SQS is a fully managed message queuing service that enables decoupling of components within distributed systems. It allows you to send, store, and receive messages between software components at any volume, without losing messages or requiring other services to be available.

Amazon SQS offers two types of message queues. Standard queues offer maximum throughput, best-effort ordering, and at-least-once delivery. Amazon SQS FIFO queues are designed to guarantee that messages are processed exactly once, in the exact order that they are sent.

---

# CLOUD FINANCIAL MANAGEMENT SERVICES

Amazon Web Services (AWS) offers several services and tools to help organizations manage and optimize their cloud finances effectively. These services enable users to gain insights into their AWS spending, set budgets, monitor costs, and optimize resource utilization.

## AWS Cost Explorer :

AWS Cost Explorer is a tool that provides comprehensive visibility into your AWS spending. It allows you to visualize and analyze your usage and costs over time, identify trends, and understand the cost drivers for your AWS services. Cost Explorer offers pre-built reports, customizable dashboards, and forecasting capabilities to help you manage and optimize your AWS spending.

## AWS Budgets :

AWS Budgets enables you to set custom budgets for your AWS spending and receive alerts when your actual spending exceeds or is forecasted to exceed your budget thresholds. You can create budgets based on specific cost dimensions, such as service, region, or tag, and monitor your spending against these budgets in real-time.

## AWS Cost and Usage Report (CUR) :

The AWS Cost and Usage Report provides detailed, granular data on your AWS usage and spending. It includes information about resource usage, costs, and metadata for each AWS service, allowing you to analyze and allocate costs accurately. You can customize the report format, frequency, and content to meet your reporting requirements.

## AWS Savings Plans :

AWS Savings Plans offer flexible pricing options for purchasing AWS compute resources (e.g., EC2 instances and Fargate tasks) at discounted rates. Savings Plans provide significant cost savings compared to On-Demand pricing, and they allow you to commit to a consistent amount of usage over a one- or three-year term.

## AWS Trusted Advisor :

AWS Trusted Advisor is a tool that provides recommendations for optimizing your AWS infrastructure in various areas, including cost optimization, performance improvement, security, and fault tolerance. It analyzes your AWS environment against best practices and offers actionable recommendations to help you reduce costs and improve efficiency.

---

# COMPUTE SERVICES

Amazon Web Services (AWS) provides a wide range of compute services that cater to different use cases, workload requirements, and performance needs. These services enable organizations to run applications, process data, and perform computational tasks in the cloud.

`INSTANCE`

-   AMAZON EC2
-   AMAZON EC2 AUTO SCALING
-   AWS BATCH

`CONTAINERS`

-   AMAZON ECS
-   AMAZON ECS ANYWHERE
-   AMAZON ECR
-   AMAZON EKS
-   AMAZON EKS ANYWHERE
-   AWS FARGATE
-   AWS APP RUNNER

`SERVERLESS`

-   AWS LAMBDA

`EDGE AND HYBRID`

-   AWS OUTPOSTS
-   AWS WAVELENGTH
-   VMWARE CLOUD ON AWS

`COST AND CAPACITY MANAGEMENT`

-   AWS SAVINGS PLAN
-   AWS BEANSTALK

## Amazon Elastic Compute Cloud (Amazon EC2):

EC2 is a web service that provides resizable compute capacity in the cloud. It allows you to launch virtual servers, known as instances, in a variety of configurations (e.g., instance type, operating system, storage, and networking). EC2 instances can be used to run a wide range of applications, from simple web servers to complex, high-performance computing (HPC) workloads.

## Amazon EC2 Auto Scaling :

Amazon EC2 Auto Scaling helps you maintain application availability and allows you to automatically add or remove EC2 instances according to conditions you define.

## AWS Batch :

Batch is a fully managed batch processing service that allows you to run batch computing workloads at any scale. It enables you to define batch jobs, specify computing resources, and schedule job execution using simple APIs or through the AWS Management Console. Batch automatically scales resources to meet demand and optimizes job scheduling for cost and performance.

## AWS App Runner :

AWS App Runner is a fully managed service that makes it easy for developers to quickly deploy containerized web applications and APIs, at scale and with no prior infrastructure experience required. Start with your source code or a container image. AWS App Runner automatically builds and deploys the web application and load balances traffic with encryption. App Runner also scales up or down automatically to meet your traffic needs. With App Runner, rather than thinking about servers or scaling, you have more time to focus on your applications.

## AWS Elastic Beanstalk :

AWS Elastic Beanstalk is a fully managed platform-as-a-service (PaaS) offering provided by Amazon Web Services (AWS) that simplifies the deployment, management, and scaling of web applications and services. It allows developers to focus on writing code without worrying about the underlying infrastructure.

You can simply upload your code, and AWS Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, and auto scaling to application health monitoring. At the same time, you retain full control over the AWS resources powering your application and can access the underlying resources at any time.

## AWS Fargate :

Fargate is a serverless compute engine for containers that allows you to run Docker containers without managing underlying infrastructure. It abstracts away the complexity of provisioning and managing servers, allowing you to focus on deploying and scaling containerized applications.

## AWS Lambda :

Lambda is a serverless computing service that allows you to run code without provisioning or managing servers. You can upload your code to Lambda and define triggers (e.g., API requests, S3 events, DynamoDB updates) to invoke your code automatically in response to events. Lambda automatically scales your code in response to incoming requests, and you only pay for the compute time consumed.

## AWS Serverless Application Repository :

The AWS Serverless Application Repository (SAR) is a managed repository of serverless applications and components that developers can use to accelerate the development of serverless applications on Amazon Web Services (AWS). It allows developers to share, discover, deploy, and reuse serverless applications and components, reducing the time and effort required to build complex serverless architectures.

Each application is packaged with an AWS Serverless Application Model (SAM) template that defines the AWS resources used.

## AWS Outposts :

AWS Outposts bring native AWS services, infrastructure, and operating models to virtually any data center, co-location space, or on-premises facility. You can use the same APIs, the same tools, the same hardware, and the same functionality across on-premises and the cloud to deliver a truly consistent hybrid experience. Outposts can be used to support workloads that need to remain on- premises due to low latency or local data processing needs.

## AWS Wavelength :

AWS Wavelength is a service provided by Amazon Web Services (AWS) that brings AWS compute and storage services to the edge of the 5G network. It allows developers to deploy their applications and workloads closer to mobile and connected devices, enabling ultra-low latency and high-bandwidth connectivity for latency-sensitive applications.

## VMware Cloud on AWS :

VMware Cloud on AWS is a jointly engineered offering by VMware and Amazon Web Services (AWS) that brings VMware's software-defined data center (SDDC) capabilities to the AWS cloud infrastructure. It seamlessly integrates VMware's compute, storage, and networking virtualization technologies with AWS's scalable and secure cloud services, enabling organizations to extend their on-premises VMware environments to the cloud without the need for costly and complex migrations or re-architecting.

## Amazon Elastic Container Service (Amazon ECS) :

Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service provided by Amazon Web Services (AWS). It allows you to run, manage, and scale Docker containers and containerized applications in the cloud with ease. Amazon ECS simplifies the process of deploying, managing, and scaling containerized workloads, enabling developers to focus on building and running applications without worrying about the underlying infrastructure.

## Amazon Elastic Kubernetes Service (Amazon EKS) :

Amazon Elastic Kubernetes Service (Amazon EKS) is a fully managed Kubernetes service provided by Amazon Web Services (AWS). It allows you to run Kubernetes clusters in the AWS cloud without having to manage the underlying infrastructure. Amazon EKS simplifies the process of deploying, managing, and scaling Kubernetes clusters, enabling you to focus on building and running containerized applications.

## Amazon Elastic Container Registry (Amazon ECR) :

Amazon Elastic Container Registry (Amazon ECR) is a fully managed container registry service provided by Amazon Web Services (AWS). It allows you to store, manage, and deploy Docker container images in a secure and scalable manner. Amazon ECR integrates seamlessly with other AWS services and container orchestration platforms, enabling you to streamline your container development and deployment workflows.

## Amazon EKS Distro :

Amazon EKS Distro (EKS-D) is a Kubernetes distribution provided by Amazon Web Services (AWS) that is based on and compatible with the same Kubernetes version that powers Amazon Elastic Kubernetes Service (Amazon EKS). EKS-D is designed to provide a consistent Kubernetes experience for customers who want to run Kubernetes clusters on their own infrastructure, either on-premises or in other cloud environments, while benefiting from the same level of security, reliability, and compatibility that Amazon EKS offers.

## Amazon EKS Anywhere :

Amazon EKS Anywhere is a new offering from Amazon Web Services (AWS) that allows customers to deploy and manage Kubernetes clusters on their own infrastructure, whether it's on-premises or in other cloud environments. With Amazon EKS Anywhere, customers can run Amazon Elastic Kubernetes Service (EKS) clusters anywhere they choose, while still benefiting from the same level of consistency, security, and operational simplicity that Amazon EKS provides in the cloud.

## Amazon ECS Anywhere :

Amazon ECS Anywhere is a new offering from Amazon Web Services (AWS) that extends the capabilities of Amazon Elastic Container Service (Amazon ECS) to enable customers to run containerized applications on any infrastructure, including on-premises, edge locations, and other cloud environments. With ECS Anywhere, customers can deploy and manage ECS tasks and services across a hybrid environment, leveraging the same ECS APIs, tools, and operational practices they use in the AWS cloud.

---

# DATABASE SERVICES :

## Amazon Relational Database Service (Amazon RDS) :

Amazon RDS is a managed relational database service that supports several popular database engines, including MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Amazon Aurora. It automates administrative tasks such as provisioning, patching, backup, recovery, and scaling, allowing you to focus on building your applications.

## Amazon Aurora:

Amazon Aurora is a fully managed MySQL and PostgreSQL-compatible relational database engine that offers high performance, scalability, and availability. It is designed to deliver up to five times the performance of standard MySQL databases and three times the performance of standard PostgreSQL databases, making it ideal for high-performance applications.

## Amazon DynamoDB:

Amazon DynamoDB is a fully managed NoSQL database service that offers seamless scalability, high availability, and low latency. It is designed to handle large-scale, high-throughput workloads with ease and provides features such as automatic scaling, encryption at rest and in transit, backup and restore, and global tables for multi-region deployments.

## Amazon ElastiCache:

Amazon ElastiCache is a fully managed in-memory caching service that supports popular caching engines such as Redis and Memcached. It allows you to deploy and manage scalable, high-performance caching clusters in the cloud, improving the speed and responsiveness of your applications by reducing latency and offloading database workloads.

## Amazon Neptune:

Amazon Neptune is a fully managed graph database service that allows you to build and run applications that work with highly connected datasets, such as social networks, recommendation engines, and fraud detection systems. It supports both the Gremlin and SPARQL query languages and provides features such as high availability, durability, and encryption.

## Amazon DocumentDB:

Amazon DocumentDB is a fully managed document database service that is compatible with MongoDB. It provides the scalability, availability, and performance of a fully managed database service while preserving the flexibility, power, and ease of use of MongoDB, making it easy for developers to migrate their MongoDB workloads to the cloud.

## Amazon Keyspaces (for Apache Cassandra):

Amazon Keyspaces is a fully managed Apache Cassandra-compatible database service that allows you to build and run applications that use Cassandra's rich data model while benefiting from the scalability, availability, and durability of AWS.

## Amazon Redshift :

Already wrote 'bout in analysis section.

## Amazon Aurora Serverless :

Amazon Aurora Serverless is a fully managed, on-demand relational database service provided by Amazon Web Services (AWS). It is designed to automatically scale compute capacity based on your application's needs, allowing you to run Aurora databases without managing traditional database instances or capacity planning.

## Amazon Quantum Ledger Database (Amazon QLDB) :

Amazon Quantum Ledger Database (Amazon QLDB) is a fully managed ledger database service provided by Amazon Web Services (AWS). It is designed to provide a transparent, immutable, and cryptographically verifiable log of all transactions in a central, scalable, and highly available database.

## Amazon Timestream :

A serverless, fully managed database service for time-series data. You can analyze trillions of events per day up to 1,000 times faster and at as little as 1/10th the cost of traditional relational databases.

# DEVELOPER TOOLS SERVICES :

## AWS X-Ray :

AWS X-Ray is a distributed tracing service provided by Amazon Web Services (AWS) that allows you to analyze and debug applications running on a distributed architecture. It provides insights into how your applications are performing and helps you identify and troubleshoot issues with latency, errors, and performance bottlenecks.

# FRONT-END WEB AND MOBILE SERVICES

## AWS Amplify:

AWS Amplify is a set of tools and services that simplify the development and deployment of full-stack applications, including front-end web and mobile apps. It provides features such as authentication, authorization, data storage, analytics, and hosting, enabling developers to build and deploy modern applications quickly.

## AWS AppSync:

AWS AppSync is a fully managed GraphQL service that developers use to build data-driven applications with real-time and offline capabilities. It enables front-end applications to interact with backend data sources, such as databases and APIs, using GraphQL queries and mutations.

## Amazon Device Farm :

Amazon Device Farm is a cloud-based mobile app testing service provided by Amazon Web Services (AWS). It allows developers to test their Android, iOS, and web applications on real devices hosted in the AWS cloud, ensuring that their apps work reliably across a wide range of devices, operating systems, and screen sizes.

# MACHINE LEARNING (ML) AND ARTIFICIAL INTELLIGENCE (AI) SERVICES

## Amazon Comprehend :

Amazon Comprehend is a fully managed natural language processing (NLP) service that uses machine learning to analyze text data and extract insights such as sentiment, entities, key phrases, language, and syntax. It supports multiple languages and can be used for tasks such as sentiment analysis, entity recognition, document classification, and topic modeling.

## Amazon Forecast:

Amazon Forecast is a fully managed service for building accurate time-series forecasting models using machine learning. It automatically analyzes historical data, identifies relevant factors, and generates forecasts with high accuracy and reliability. Forecast can be used for demand forecasting, sales forecasting, inventory planning, and other predictive analytics tasks.

## Amazon Lex:

Amazon Lex is a fully managed service for building conversational interfaces using natural language understanding (NLU) and speech recognition technologies. It provides pre-built models for common use cases such as chatbots, virtual agents, and interactive voice response (IVR) systems, as well as customization options for training custom models.

## Amazon Polly :

Amazon Polly is a fully managed text-to-speech (TTS) service that uses advanced deep learning technologies to generate lifelike speech from text. It supports multiple languages and voices, as well as customization options for voice style, pronunciation, and speech rate. Polly can be used to create interactive voice response (IVR) systems, virtual assistants, audiobooks, and more.

## Amazon Rekognition :

Amazon Rekognition is a fully managed computer vision service that provides deep learning-based image and video analysis. It can identify objects, people, text, scenes, and activities in images and videos, as well as detect faces, recognize celebrities, and analyze emotions. Rekognition is commonly used for applications such as content moderation, facial recognition, object detection, and video analysis.

## Amazon SageMaker:

Amazon SageMaker is a fully managed service for building, training, and deploying machine learning models at scale. It provides a complete set of tools and workflows for every step of the ML lifecycle, including data preparation, model training, hyperparameter tuning, and model deployment. SageMaker supports popular ML frameworks like TensorFlow, PyTorch, and Apache MXNet, as well as built-in algorithms and pre-trained models.

## Amazon Kendra :

AWS Kendra is an intelligent search service provided by Amazon Web Services (AWS) that makes it easy for organizations to find information stored across multiple sources within their enterprise. It uses machine learning algorithms to index and search data from various repositories, such as databases, file systems, websites, and more, allowing users to quickly find the information they need.

## Amazon Textract :

Amazon Textract is a machine learning service provided by Amazon Web Services (AWS) that automatically extracts text and data from scanned documents, PDFs, and images. It uses advanced optical character recognition (OCR) technology to analyze documents and extract structured data, such as text, tables, and forms, making it easier to search, analyze, and process large volumes of documents.

## Amazon Fraud Detector :

Amazon Fraud Detector is a fully managed service provided by Amazon Web Services (AWS) that helps organizations detect and prevent fraud in their applications and systems. It uses machine learning (ML) techniques to analyze transactions, identify patterns, and detect suspicious activities in real-time, enabling organizations to mitigate fraud risks and protect against financial losses.

## Amazon Transcribe :

Amazon Transcribe is a fully managed automatic speech recognition (ASR) service provided by Amazon Web Services (AWS). It enables developers to easily convert speech to text in real-time or batch mode, making it easier to transcribe audio recordings, videos, call center conversations, and other spoken content into written text.

## Amazon Translate :

Amazon Translate is a machine translation service provided by Amazon Web Services (AWS) that enables developers to easily translate text between languages with high accuracy and low latency. It uses advanced neural machine translation (NMT) models to provide fast and accurate translations for a wide range of languages and text types.

---

# MANAGEMENT AND GOVERNANCE SERVICES

## AWS Auto Scaling :

AWS Auto Scaling is a service provided by Amazon Web Services (AWS) that enables organizations to automatically adjust the capacity of their AWS resources to meet changing demand and optimize performance, availability, and cost. It helps ensure that applications can automatically scale up or down based on factors such as traffic patterns, resource utilization, and performance metrics, without manual intervention.

## AWS CloudFormation :

AWS CloudFormation is a service provided by Amazon Web Services (AWS) that enables developers and system administrators to provision and manage AWS infrastructure resources in a declarative and automated manner. It allows users to define their infrastructure as code using JSON or YAML templates, called CloudFormation templates, and then use these templates to create, update, and delete AWS resources in a repeatable and consistent way.

## AWS CloudTrail :

AWS CloudTrail is a service provided by Amazon Web Services (AWS) that enables organizations to monitor, audit, and log AWS account activity and resource usage. It records API calls and actions taken by users, applications, and AWS services within an AWS account, providing a comprehensive trail of events for security analysis, compliance auditing, and troubleshooting purposes.

## Amazon CloudWatch :

Amazon CloudWatch is a monitoring and observability service provided by Amazon Web Services (AWS) that enables organizations to collect, analyze, and visualize metrics, logs, and events from their AWS resources and applications in real-time. CloudWatch helps organizations monitor the performance, health, and operational status of their AWS infrastructure, applications, and services, and take proactive actions to troubleshoot issues and optimize performance.

## AWS Compute Optimizer :

AWS Compute Optimizer is a service provided by Amazon Web Services (AWS) that helps customers optimize the performance, cost, and resources of their AWS EC2 instances. It analyzes historical usage patterns and resource configurations to provide recommendations for improving the performance and efficiency of EC2 instances, including recommendations for right-sizing instances, selecting optimal instance types, and identifying opportunities for cost savings.

## AWS Control Tower :

AWS Control Tower is a service provided by Amazon Web Services (AWS) that simplifies the process of setting up and governing a secure, multi-account AWS environment based on AWS best practices and industry standards. It provides a centralized dashboard and set of pre-configured guardrails and policies to help customers establish a well-architected AWS environment that meets security, compliance, and operational requirements.

## AWS Config :

AWS Config is a service provided by Amazon Web Services (AWS) that enables customers to assess, audit, and evaluate the configuration of their AWS resources continuously. It provides visibility into the configuration changes of AWS resources over time, helps customers assess resource compliance against predefined rules and policies, and enables them to monitor resource configuration changes for security, compliance, and operational purposes.

## AWS Health Dashboard :

The AWS Health Dashboard is a service provided by Amazon Web Services (AWS) that provides customers with real-time visibility into the operational status and health of their AWS resources and services. It offers a centralized view of the current status of AWS services, including information about service disruptions, performance issues, and planned maintenance events, helping customers stay informed about the availability and reliability of their AWS infrastructure.

## AWS License Manager :

AWS License Manager is a service provided by Amazon Web Services (AWS) that helps organizations manage software licenses and enforce license usage policies in their AWS environments. It enables customers to manage software licenses from vendors such as Microsoft, SAP, Oracle, IBM, and others, across their AWS accounts and instances, helping them optimize license usage, reduce costs, and maintain compliance with licensing agreements and regulations.

## Amazon Managed Grafana :

Amazon Managed Grafana is a fully managed service provided by Amazon Web Services (AWS) that simplifies the deployment, configuration, and management of Grafana for visualizing and monitoring metrics, logs, and data from various sources. Grafana is an open-source analytics and visualization platform commonly used for monitoring and observability in cloud environments.

## Amazon Managed Service for Prometheus :

Amazon Managed Service for Prometheus (AMP) is a fully managed Prometheus-compatible monitoring service provided by Amazon Web Services (AWS). Prometheus is an open-source monitoring and alerting toolkit that is widely used for collecting and querying metrics from various sources in cloud-native environments. AMP simplifies the deployment, scaling, and management of Prometheus infrastructure, allowing customers to monitor their applications and infrastructure on AWS with ease.

## AWS Organizations :

AWS Organizations is a service provided by Amazon Web Services (AWS) that helps customers centrally manage and govern multiple AWS accounts in their organization. It simplifies the management of AWS resources, access controls, and policies across accounts, enabling customers to scale their AWS environments securely and efficiently.

## AWS Proton :

AWS Proton is a fully managed service provided by Amazon Web Services (AWS) that simplifies and automates the process of deploying, managing, and scaling containerized and serverless applications. It helps development teams streamline the application deployment process by providing a set of tools, templates, and best practices for building and managing infrastructure as code (IaC) workflows.

## Service Catalog :

AWS Service Catalog is a service provided by Amazon Web Services (AWS) that enables organizations to create and manage catalogs of approved IT services, resources, and applications for use within their AWS environments. It helps organizations standardize and govern the deployment of AWS resources and applications, enforce compliance with organizational policies, and improve operational efficiency and consistency.

## AWS Systems Manager :

AWS Systems Manager is a management service provided by Amazon Web Services (AWS) that helps customers manage and automate operational tasks across their AWS infrastructure and resources. It provides a unified interface for managing instances, virtual machines, containers, applications, and other AWS resources, enabling customers to simplify and streamline their operations management workflows.

## AWS Trusted Advisor :

AWS Trusted Advisor is a service provided by Amazon Web Services (AWS) that offers guidance and recommendations to help customers optimize their AWS environments for performance, security, reliability, and cost-effectiveness. Trusted Advisor analyzes customers' AWS accounts and provides actionable recommendations based on AWS best practices and architectural principles, helping customers improve their infrastructure, reduce costs, and enhance their overall AWS experience.

## AWS Well-Architected Tool :

The AWS Well-Architected Tool is a service provided by Amazon Web Services (AWS) that helps customers assess the architecture of their AWS workloads against AWS best practices and architectural principles. It provides a framework and methodology for evaluating the reliability, performance, security, cost optimization, and operational excellence of AWS workloads, enabling customers to identify areas for improvement and implement architectural changes to align with best practices.

---

# MEDIA SERVICES

## Amazon Elastic Transcoder :

Amazon Elastic Transcoder is a cloud-based media transcoding service provided by Amazon Web Services (AWS) that enables customers to convert media files from one format to another. It simplifies the process of transcoding video and audio files for playback across different devices, platforms, and screen sizes, allowing customers to deliver high-quality multimedia content to their users efficiently and cost-effectively.

## Amazon Kinesis Video Streams :

Done already.

---

# MIGRATION AND TRANSFER

## AWS Application Discovery Service :

The AWS Application Discovery Service is a tool provided by Amazon Web Services (AWS) that helps customers plan migration projects by identifying applications and dependencies in their on-premises data centers. It automates the process of discovering and collecting configuration, usage, and dependency data for servers, virtual machines, and applications running in a customer's environment.

## AWS Application Migration Service :

AWS Application Migration Service, previously known as CloudEndure Migration, is a service provided by Amazon Web Services (AWS) that helps customers migrate their on-premises applications to AWS quickly, securely, and with minimal disruption. It automates the process of replicating and migrating applications, servers, and data from on-premises environments to AWS infrastructure, enabling customers to accelerate their cloud migration projects.

## AWS Database Migration Service :

The AWS Database Migration Service (DMS) is a fully managed service provided by Amazon Web Services (AWS) that enables customers to migrate their databases to AWS quickly, securely, and with minimal downtime. It supports heterogeneous database migrations, allowing customers to move data between different database engines and platforms seamlessly.

## AWS Migration Hub :

AWS Migration Hub is a service provided by Amazon Web Services (AWS) that enables customers to plan and track the progress of their application migrations to the AWS Cloud. It provides a centralized dashboard and management interface for managing multiple migration projects, tracking the status of migration tasks, and accessing key migration resources and tools.

## AWS Snow Family :

The AWS Snow Family is a collection of physical devices provided by Amazon Web Services (AWS) that enable customers to securely transfer large amounts of data between their on-premises environments and the AWS Cloud, even in environments with limited or no network connectivity.

## AWS DataSync :

AWS DataSync is a fully managed data transfer service provided by Amazon Web Services (AWS) that simplifies and accelerates the process of transferring data between on-premises storage systems and AWS storage services. It is designed to securely and efficiently move large volumes of data over the network, enabling customers to migrate data to AWS, replicate data between storage systems, and synchronize data for backup and disaster recovery purposes.

## AWS Transfer Family :

The AWS Transfer Family is a set of fully managed file transfer services provided by Amazon Web Services (AWS) that enables customers to securely transfer files over the internet and integrate file transfer capabilities into their applications and workflows. The AWS Transfer Family offers two main services: AWS Transfer for SFTP and AWS Transfer for FTPS.

---

# NETWORKING AND CONTENT DELIVERY

## Amazon API Gateway :

Amazon API Gateway is a fully managed service provided by Amazon Web Services (AWS) that enables customers to create, publish, maintain, monitor, and secure APIs (Application Programming Interfaces) at scale. It acts as a front-door for backend services, allowing customers to expose their application logic and data to external clients, such as web and mobile applications, third-party developers, and partner systems, via HTTP and WebSocket protocols.

## Amazon CloudFront :

Amazon CloudFront is a content delivery network (CDN) service provided by Amazon Web Services (AWS) that delivers static and dynamic web content, including images, videos, applications, APIs, and other assets, to users around the world with low latency and high transfer speeds. It accelerates the delivery of content by caching it at edge locations located closer to end-users, reducing the distance and network latency between users and origin servers.

## Amazon Route 53 :

Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service provided by Amazon Web Services (AWS). It is designed to route end users to internet applications by translating human-readable domain names (such as www.example.com) into numeric IP addresses (such as 192.0.2.1) that computers use to connect to each other. Route 53 also provides DNS-based load balancing and health checking capabilities to improve the availability, performance, and reliability of internet-facing applications and websites.

## Amazon Virtual Private Cloud (Amazon VPC) :

Amazon Virtual Private Cloud (Amazon VPC) is a service provided by Amazon Web Services (AWS) that enables customers to create and manage isolated virtual networks within the AWS cloud environment. Amazon VPC allows customers to define their own virtual network topology, including IP address ranges, subnets, route tables, and network access controls, providing a high level of control and customization over their cloud infrastructure.

## AWS Direct Connect :

AWS Direct Connect is a network service provided by Amazon Web Services (AWS) that enables customers to establish dedicated and private network connections between their on-premises data centers, office locations, or co-location environments and the AWS cloud. It bypasses the public internet, providing a more reliable, consistent, and secure connection for accessing AWS resources and services.

## AWS Global Accelerator :

AWS Global Accelerator is a networking service provided by Amazon Web Services (AWS) that improves the availability and performance of internet applications and services for global users. It uses the AWS global network infrastructure to optimize the routing of traffic and dynamically route requests to the nearest AWS edge location, reducing latency and improving the user experience.

## AWS PrivateLink :

AWS PrivateLink is a networking service provided by Amazon Web Services (AWS) that enables customers to securely connect their Virtual Private Cloud (VPC) to supported AWS services and endpoints without exposing traffic to the public internet. It facilitates private connectivity between VPCs and AWS services or endpoints hosted by other AWS accounts or AWS Marketplace vendors.

## AWS Transit Gateway :

AWS Transit Gateway is a fully managed service provided by Amazon Web Services (AWS) that simplifies network connectivity and routing for Amazon Virtual Private Clouds (VPCs), on-premises networks, and AWS services. It acts as a hub that connects multiple VPCs and on-premises networks, allowing customers to centrally manage and scale their network infrastructure in a simplified and cost-effective manner.

## AWS VPN :

AWS VPN is a service provided by Amazon Web Services (AWS) that allows customers to establish secure and private connections between their on-premises networks, remote offices, or individual devices and their Amazon Virtual Private Clouds (VPCs) in the AWS cloud. It enables encrypted communication over the public internet, providing secure access to AWS resources and services without exposing sensitive data to potential security threats.

## Elastic Load Balancing :

Elastic Load Balancing (ELB) is a service provided by Amazon Web Services (AWS) that automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions, to ensure high availability, fault tolerance, and scalability for applications and services deployed in the AWS cloud.

---

# SECURITY , IDENTITY AND COMPLIANCE

## Amazon Cognito :

Amazon Cognito is a service provided by Amazon Web Services (AWS) that enables developers to add user sign-up, sign-in, and access control functionalities to web and mobile applications. It simplifies the process of managing user identities, authentication, authorization, and user data synchronization, allowing developers to focus on building engaging and secure applications without having to deal with the complexities of identity management.

## Amazon Detective :

Amazon Detective is a security service provided by Amazon Web Services (AWS) that helps customers analyze, investigate, and identify security issues and anomalies in their AWS accounts and workloads. It collects, aggregates, and analyzes log data from various AWS services and resources, providing insights and visualizations to help customers understand and respond to security threats effectively.

## Amazon GuardDuty :

Amazon GuardDuty is a threat detection service provided by Amazon Web Services (AWS) that helps customers protect their AWS accounts and workloads by continuously monitoring for malicious activity and unauthorized behavior. It analyzes log data from various AWS services, such as AWS CloudTrail, Amazon VPC Flow Logs, and DNS logs, to identify potential security threats and vulnerabilities.

## Amazon Inspector :

Amazon Inspector is an automated security assessment service provided by Amazon Web Services (AWS) that helps customers improve the security and compliance of their AWS resources and applications. It analyzes the security posture of EC2 instances and other resources within AWS environments, identifying security vulnerabilities, configuration issues, and potential security risks.

## Amazon Macie :

Amazon Macie is a security service provided by Amazon Web Services (AWS) that helps customers discover, classify, and protect sensitive data stored in AWS environments. It uses machine learning and pattern recognition techniques to automatically identify and classify sensitive data, such as personally identifiable information (PII), intellectual property, and confidential documents, helping customers improve data security and compliance.

## AWS Artifact :

AWS Artifact is a centralized repository of compliance and security-related documentation provided by Amazon Web Services (AWS). It offers easy access to various types of documentation, such as compliance reports, third-party audit certifications, and agreements with AWS.

## AWS Audit Manager :

AWS Audit Manager is a service provided by Amazon Web Services (AWS) that helps customers automate the process of auditing their AWS usage and compliance with regulatory standards and industry best practices. It enables customers to manage, automate, and streamline their audit workflows, including the assessment of AWS resources, controls, and security configurations.

## AWS Certificate Manager :

AWS Certificate Manager (ACM) is a service provided by Amazon Web Services (AWS) that simplifies the management and provisioning of SSL/TLS certificates for use with AWS services and resources. It enables customers to secure their websites, applications, and services with SSL/TLS encryption, without the need to manage the complexities of certificate issuance, renewal, and deployment.

## AWS CloudHSM :

AWS CloudHSM (Hardware Security Module) is a service provided by Amazon Web Services (AWS) that enables customers to generate, store, and manage cryptographic keys and perform cryptographic operations in a secure hardware environment. It helps customers meet regulatory and compliance requirements, protect sensitive data, and enhance the security of their applications and workloads.

## AWS Directory Service :

AWS Directory Service is a managed service provided by Amazon Web Services (AWS) that enables customers to set up and manage directories in the AWS Cloud, allowing them to integrate their existing on-premises directories or create new directories for user authentication and authorization.

## AWS Firewall Manager :

AWS Firewall Manager is a managed service provided by Amazon Web Services (AWS) that helps customers centrally manage and configure firewall rules across multiple AWS accounts and resources. It enables organizations to enforce security policies, ensure compliance, and protect their AWS environments from unauthorized access and potential security threats.

## AWS Identity and Access Management :

AWS Identity and Access Management (IAM) is a web service provided by Amazon Web Services (AWS) that enables customers to securely manage access to AWS services and resources. IAM allows customers to create and manage users, groups, roles, and permissions, controlling who can access specific resources and what actions they can perform.

## AWS Key Management Service :

AWS Key Management Service (KMS) is a managed service provided by Amazon Web Services (AWS) that allows customers to create and manage cryptographic keys for encrypting and decrypting their data. It helps customers protect their data and meet compliance requirements by providing a secure and scalable solution for managing encryption keys.

## AWS Network Firewall :

AWS Network Firewall is a managed firewall service provided by Amazon Web Services (AWS) that enables customers to monitor and filter network traffic to and from their AWS resources. It allows customers to create and enforce firewall rules to control traffic at the network and application layers, protecting their applications and workloads from unauthorized access, threats, and malicious activity.

## AWS Resource Access Manager :

AWS Resource Access Manager (RAM) is a service provided by Amazon Web Services (AWS) that enables customers to share AWS resources with other AWS accounts within the same organization or across multiple AWS accounts. It allows customers to centrally manage and control access to shared resources, simplifying resource sharing and collaboration across organizational boundaries.

## AWS Secrets Manager :

AWS Secrets Manager is a service provided by Amazon Web Services (AWS) that enables customers to securely store, manage, and rotate sensitive information, such as passwords, API keys, and encryption keys. It helps customers protect their credentials and other secrets by providing a centralized and secure storage solution with built-in encryption, access controls, and automatic rotation capabilities.

## AWS Security Hub :

AWS Security Hub is a security and compliance service provided by Amazon Web Services (AWS) that helps customers centrally manage and automate their security posture across their AWS accounts and resources. It aggregates, organizes, and prioritizes security findings from various AWS services and third-party security tools, providing customers with a comprehensive view of their security alerts and compliance status.

## AWS Shield :

AWS Shield is a managed Distributed Denial of Service (DDoS) protection service provided by Amazon Web Services (AWS). It helps customers protect their web applications and workloads against the impact of DDoS attacks by providing automatic detection and mitigation capabilities.

## AWS IAM Identity Center :

As of my last update in January 2022, there's no service called "AWS IAM Identity Center." It's possible that it could be a new service introduced after that date, or it might refer to a feature or concept within AWS Identity and Access Management (IAM).

IAM is the service provided by Amazon Web Services (AWS) that enables customers to manage user identities and permissions for accessing AWS services and resources securely. It allows users to create and manage IAM users, groups, roles, and policies to control access to AWS resources.

## AWS WAF :

AWS WAF (Web Application Firewall) is a web application firewall service provided by Amazon Web Services (AWS) that helps protect web applications from common web exploits and security vulnerabilities. It allows customers to define customizable rules to filter and monitor HTTP and HTTPS requests to their web applications, providing protection against threats such as SQL injection, cross-site scripting (XSS), and distributed denial-of-service (DDoS) attacks.

## AWS Backup :

AWS Backup is a fully managed backup service provided by Amazon Web Services (AWS) that simplifies the process of backing up and restoring data across AWS services and resources. It enables customers to centrally manage and automate backup tasks for their databases, file systems, volumes, and other AWS resources, helping them protect their data and ensure business continuity.

## Amazon Elastic Block Store :

Amazon Elastic Block Store (Amazon EBS) is a block-level storage service provided by Amazon Web Services (AWS) that offers persistent block storage volumes for use with Amazon EC2 (Elastic Compute Cloud) instances. It allows customers to create and attach storage volumes to their EC2 instances to store data, databases, and operating systems.

## Amazon Elastic File System :

Amazon Elastic File System (Amazon EFS) is a fully managed, scalable file storage service provided by Amazon Web Services (AWS) that enables customers to create and manage file systems that can be accessed concurrently by multiple Amazon EC2 instances and on-premises servers. It provides scalable, highly available, and durable file storage for a wide range of use cases, including content repositories, shared file storage, and application data storage.

## Amazon FSx for Lustre :

Amazon FSx for Lustre is a high-performance file system service provided by Amazon Web Services (AWS) that is optimized for processing large-scale, compute-intensive workloads such as machine learning, high-performance computing (HPC), and data analytics. It allows customers to easily create and deploy Lustre file systems in the AWS Cloud, providing scalable, high-throughput storage for processing and analyzing large datasets.

## Amazon FSx for Windows File Server :

Amazon FSx for Windows File Server is a fully managed file storage service provided by Amazon Web Services (AWS) that offers native support for Windows file shares, allowing customers to easily deploy and manage Windows-based file storage in the AWS Cloud. It provides fully managed Windows file servers with support for common file sharing protocols and features, such as SMB (Server Message Block) and Active Directory integration.

## Amazon Simple Storage Service :

Amazon Simple Storage Service (Amazon S3) is an object storage service provided by Amazon Web Services (AWS) that offers scalable, durable, and secure storage for a wide variety of data types, including images, videos, documents, backups, and application data. Amazon S3 allows customers to store and retrieve any amount of data from anywhere on the web, making it a highly versatile and widely used storage solution.

## AWS Storage Gateway :

AWS Storage Gateway is a hybrid storage service provided by Amazon Web Services (AWS) that enables customers to seamlessly integrate on-premises environments with cloud storage. It facilitates hybrid cloud storage solutions by connecting on-premises applications and storage systems with cloud-based storage services, such as Amazon S3, Amazon Glacier, and AWS Storage Gateway volumes.
