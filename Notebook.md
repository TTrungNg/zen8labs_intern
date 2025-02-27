# zen8labs_intern: AWS Cloud Practitioner


## Table of Contents
I. INTRODUCTION TO AWS
II. COMPUTE IN THE CLOUD
III. GLOBAL INFRASTRUCTURE AND RELIABILITY
IV. NETWORKING
V. STORAGE AND DATABASES

## Contents

#### I. INTRODUCTION TO AWS

*   Key concept: **“Pay as you go”** => In real world, there are times that requests from users get higher, aws can serve more computer at that time with one click. And then when requests back to normal, those added computer can be taken away.
*   Why aws have many services ? Because companies need all of those. Aws want to make stuffs duplicated which make no diffrientiator easily for every customer (like installing a MySQL DB).
*   The **three cloud computing deployment models** are **cloud-based, on-premises, and hybrid**:

| **cloud-based**                                                              | **on-premises**                                                                                               | **hybrid**                                                                 |
| :--------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------- |
| Run all parts of the application in the cloud.                           | Deploy resources by using virtualization and resource management tools.                                     | Connect cloud-based resources to on-premises infrastructure.         |
| Migrate existing applications to the cloud.                              | Increase resource utilization by using application management and virtualization technologies.           | Integrate cloud-based resources with legacy IT applications.          |
| Design and build new applications in the cloud.                          |                                                                                                               |                                                                            |

*   **Benefits of cloud computing**:
    *   Trade capital expense for variable expense
    *   Benefit from massive economies of scale
    *   Stop guessing capacity
    *   Increase speed and agility
    *   Stop spending money running and maintaining data centers
    *   Go global in minutes

#### II. COMPUTE IN THE CLOUD

*   **Multitenancy:** Sharing underlying hardware between virtual machines. The hypervisor is responsible for managing each EC2 instances secured from any other ones on a host. The resources of the physical server is also shared and managed.
*   EC2 has wide range of configs like OS, internal business apps, simple or complex web apps, db or third-party software,…
*   **Vertical scaling an instance** (resizable compute capacity): start with a small instance and give it more memory and cpu when the app max out that server.
*   *(Optional) Networking aspect of EC2: types of requests make it to server, publicly or privately accessible.*
*   5 Types of EC2 instance:
    *   **General purpose instances:**

    | Provide a balance of compute, memory, and networking resources. | Application servers, gaming servers, backend servers for enterprise applications, small and medium databases. |
    | :------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------- |
    *   **Compute optimized instances:**

    | Ideal for compute-bound applications that benefit from high-performance processors. *Also use for batch processing workloads that require processing many transactions in a single group.* | web, application, and gaming servers. |
    | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------- |
    *   **Memory optimized instances:**

    | Fast performance for workloads that process large datasets in memory | Requires large amounts of data to be preloaded before running an application |
    | :---------------------------------------------------------------------- | :---------------------------------------------------------------------------------- |
    *   **Accelerated computing instances:**

    | Use hardware accelerators, or coprocessors, to perform some functions more efficiently than is possible in software running on CPUs. | floating-point number calculations, graphics processing, and data pattern matching. |
    | :------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------- |
    | In computing, a hardware accelerator is a component that can expedite data processing.                                                 | workloads such as graphics applications, game streaming, and application streaming.   |
    *   **Storage optimized instances**

    | Designed for workloads that require high, sequential read and write access to large datasets on local storage | input/output operations per second (IOPS) |
    | :------------------------------------------------------------------------------------------------------------------ | :--------------------------------------------- |
*   5 types of Pricing:

| **Feature**          | **On-Demand Instances**                   | **Reserved Instances (RI)**                                  | **Savings Plans**                                                      | **Spot Instances**                               | **Dedicated Hosts**                                   |
| :------------------- | :---------------------------------------- | :----------------------------------------------------------- | :--------------------------------------------------------------------- | :----------------------------------------------- | :---------------------------------------------------- |
| **Pricing Model**    | Pay per hour or per second, no commitment | Discounted pricing with 1-year or 3-year commitment       | Discounted pricing with 1-year or 3-year commitment                 | Hourly price based on long-term supply and demand. | Per Hour(On-Demand) or 1-3 year commitment (Reservation) |
| **Discount**         | No discount, full On-Demand rates       | Up to **72%** discount (Standard RI)                     | Up to **72%** discount                                             | Up to 90% discount                         | None                                            |
| **Flexibility**      | Most flexible, can change instance type and Region anytime | Limited to specific instance type, OS, and tenancy, Region         | More flexible than **RI**, applies to any instance size, OS, or tenancy within the same instance family and Region | Wait till EC2 capacity available             | Most Flexible                                   |
| **Capacity Reservation** | No reservation, capacity not guaranteed   | Available only if assigned to a specific AZ                 | **Not available**                                                    | Not available                            | Available                                       |
| **Usage Commitment** | None, pay as you go                   | Must commit to a fixed **instance type and size**         | Commit to a **spending amount per hour** instead of instance type | None                                       | Optional                                        |
| **Best Use Case**    | Short-term, unpredictable workloads      | Steady-state workloads with known requirements             | Flexible workloads where instance type/size may change             | Workloads with flexible start and end times    | When having compliance requirements             |
| **Example**          | Running an EC2 instance temporarily for testing | Running a web server 24/7 with a fixed instance type         | Running various EC2 instances within an instance family in a Region             | Data processing job for a customer survey   | Medicine data cannot be on shared cloud        |
*   **EC2 Auto Scaling:** add new instances to the application when necessary and terminate them when no longer needed.
*Minimum, Desired, Maximum EC2 instances can be set in AutoScale Config.*
*   **Elastic Load Balancing(ELB):** automatically distributes incoming application traffic across multiple resources, such as Amazon EC2 instances.
*Note: Instead of taking a look to every EC2 instances to check if it is available, the request con go straightly to the ELB, and take route directly to the available EC2 Instance.*
*   Microservices approach is used with services and components. There are two services to help it: Amazon Simple Notification Service (Amazon SNS) and Amazon Simple Queue Service (Amazon SQS).

**Amazon SNS** is a publish/subscribe service. Using Amazon SNS topics, a publisher publishes messages to subscribers. Subscribers can be web servers, email addresses, AWS Lambda functions, or several other options.

**Using Amazon SQS**, you can send, store, and receive messages between software components, without losing messages or requiring other services to be available. In Amazon SQS, an application sends messages into a queue. A user or service retrieves a message from the queue, processes it, and then deletes it from the queue.
*   **AWS Lambda** is a service that lets you run code without needing to provision or manage servers.
*   **Amazon Elastic Container Service (Amazon ECS):** highly scalable, high-performance container management system that enables you to run and scale containerized applications on AWS which support Docker.
*   **Amazon Elastic Kubernetes Service (Amazon EKS):** is a fully managed service that you can use to run Kubernetes on AWS.
*   **AWS Fargate:** a serverless compute engine for containers. It works with both Amazon ECS and Amazon EKS. Don’t need to manage servers. Pay only for the resources that are required to run containers.

#### III. GLOBAL INFRASTRUCTURE AND RELIABILITY

*   Determining the right **Region**:

    *   Compliance with data governance and legal requirements
    *   Proximity to your customers: reduce latency.
    *   Available services within a Region: Not every Region has the same services (especially new services)
    *   Pricing: Region prices are different (Because of Tax, etc)
*   An **Availability Zone** is a single data center or a group of data centers within a Region. Availability Zones are located tens of miles apart from each other. This is close enough to have low latency (the time between when content requested and received) between Availability Zones. However, if a disaster occurs in one part of the Region, they are distant enough to reduce the chance that multiple Availability Zones are affected.
*   An **edge location** is a site that Amazon CloudFront uses to store cached copies of your content closer to your customers for faster delivery.
*   3 ways to interact with AWS services:
    *   **AWS Management Console** is a web-based interface for accessing and managing AWS services. You can quickly access recently used services and search for other services by name, keyword, or acronym. The console includes wizards and automated workflows that can simplify the process of completing tasks.
    *   **WS Command Line Interface (AWS CLI):** control directly from the command line within one tool.
    *   **Software development kits (SDKs)** : make it easier for you to use AWS services through an API designed for your programming language or platform.
*   2 more ways to interact with AWS: Elastic Beanstalk and CloudFormation:

| **Criteria**         | **AWS Elastic Beanstalk**                                       | **AWS CloudFormation**                                                                        |
| :------------------- | :-------------------------------------------------------------- | :-------------------------------------------------------------------------------------------- |
| **Primary Purpose**  | Automatically deploy and manage applications.                   | Manage AWS infrastructure as code (IaC).                                                    |
| **How It Works**     | Users upload an application, and Beanstalk automatically provisions the required infrastructure. | Users define AWS resources using YAML/JSON templates.                                         |
| **Customization Level** | Limited, as Beanstalk handles most infrastructure automatically. | Highly flexible, allowing complex infrastructure configurations.                            |
| **Application Deployment** | Built-in CI/CD pipeline, automatically deploys new versions.     | Does not deploy applications automatically, only manages infrastructure.                    |
| **Scalability**      | Automatically scales resources based on application load.         | Does not automatically scale, but can configure Auto Scaling.                               |
| **Complexity**       | Easy to use, requires minimal infrastructure knowledge.         | Requires AWS expertise and writing YAML/JSON templates.                                     |
| **Best Use Cases**   | Quickly deploying web applications without managing infrastructure. | Managing and automating AWS infrastructure using IaC.                                       |
| **Cost**             | Only charges for AWS resources used.                            | Only charges for AWS resources used (CloudFormation itself is free).                        |

#### IV. NETWORKING

*   **Amazon Virtual Private Cloud (VPC)** : establish boundaries around your AWS resources. In this, you can launch resources in a virtual network that you define (public or private). Within a virtual private cloud (VPC), you can organize your resources into subnets. A **subnet** is a section of a VPC that can contain resources such as Amazon EC2 instances.
*   **Internet Gateway (IGW):** allow public traffic from the internet to access your VPC (without this, no one can access aws resources).
*   **Virtual Private Gateway:** because of this, only connection with VPN or protection can access private resources in VPC. This one is best when we have connection between an on-premises data center or internal corporate network and our VPC.
*   **AWS Direct Connect:** establish a dedicated private connection between your data center and a VPC. This is best when we need to reduce network costs and more bandwidth. (Like make our own way directly to the VPC from the data center)
*   **Subnet:** is a section of a VPC in which you can group resources based on security or operational needs. Subnets can be public or private. 2 types:
    *   **Public subnets** contain resources that need to be accessible by the public, such as an online store’s website.
    *   **Private subnets** contain resources that should be accessible only through your private network, such as a database that contains customers’ personal information and order histories.
*   **Network Access Control List(ACL)** : a virtual firewall that controls inbound and outbound traffic at the subnet level.
    *   When configuring your VPC, you can use your account’s default network ACL or create custom network ACLs.
    *   **Your account’s default** network ACL **allows** all inbound and outbound traffic, but you can modify it by adding your own rules.
    *   For **custom network ACLs**, all inbound and outbound traffic is **denied** until you add rules to specify which traffic to allow.
*   **Stateless packet filtering** : Network ACLs perform **stateless** packet filtering. They remember nothing and check packets that cross the subnet border each way: inbound and outbound.
*   **Security groups:** A security group is a virtual firewall that controls inbound and outbound traffic for an Amazon EC2 instance. *By default, a security group denies all inbound traffic and allows all outbound traffic. You can add custom rules to configure which traffic should be allowed; any other traffic would then be denied*
*   **Stateful packet filtering:** Security groups perform **stateful** packet filtering. They remember previous decisions made for incoming packets.
*   *Domain Name System(DNS)*: DNS like the phone book of the internet. DNS resolution is the process of translating a domain name to an IP address.
*   **Amazon Route 53:** is a DNS web service. It gives developers and businesses a reliable way to route end users to internet applications hosted in AWS.
    *   Connects user requests to infrastructure running in AWS (such as Amazon EC2 instances and load balancers). It can route users to infrastructure outside of AWS.
    *   Also manage the DNS records for domain names. You can register new domain names directly in Route 53. You can also transfer DNS records for existing domain names managed by other domain registrars.

#### V. STORAGE AND DATABASES

*   **Instance Stores:** provides temporary block-level storage for an Amazon EC2 instance. It is physically attached to the host computer for an EC2 instance, and therefore has the same lifespan as the instance. When the instance is terminated, you lose any data in the instance store.
*   **Amazon Elastic Block Store (EBS):** a service that provides block-level storage volumes that you can use with Amazon EC2 instances.
    *   If you stop or terminate an Amazon EC2 instance, all the data on the attached EBS volume remains available.
    *   To create an EBS volume, you define the configuration (such as volume size and type) and provision it.
*   **Amazon EBS snapshots:** an incremental backup. This means that the first backup taken of a volume copies all the data. For subsequent backups, only the blocks of data that have changed since the most recent snapshot are saved.
*   8 S3 storage classes:

| **Storage Class**              | **Availability Zones** | **Access Frequency**         | **Cost Structure**                                                                        | **Retrieval Time** | **Use Cases**                                                                                                                                                                                                                                               |
| :----------------------------- | :----------------------- | :--------------------------- | :---------------------------------------------------------------------------------------- | :----------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **S3 Standard**                | ≥3                       | Frequently accessed          | **NOT SURE**                                                                                | Immediate          | Websites, content distribution, analytics                                                                                                                                                                                                   |
| **S3 Standard-IA**             | ≥3                       | Infrequently accessed        | Lower storage cost, higher retrieval cost                                                 | Immediate          | Backup, disaster recovery                                                                                                                                                                                                                 |
| **S3 One Zone-IA**             | 1                        | Infrequently accessed        | Lower storage cost than **S3 Standard-IA**                                                 | Immediate          | Cost-saving for non-critical data                                                                                                                                                                                                         |
| **S3 Intelligent-Tiering**     | ≥3                       | Unknown/changing access patterns | Small monthly monitoring and automation fee **per object**                                  | Immediate          | Data with unpredictable access patterns. S3 Intelligent-Tiering automatically moves objects accessed in 30 days to the infrequent access tier, **S3 Standard-IA**. In opposites, the ones accessed are moved to frequent access tier, **S3 Standard**. |
| **S3 Glacier Instant Retrieval** | ≥3                       | Infrequently accessed        | Low storage cost, higher retrieval cost                                                 | Milliseconds       | Archive requiring quick access                                                                                                                                                                                                            |
| **S3 Glacier Flexible Retrieval** | ≥3                       | Infrequently accessed        | Very low storage cost, variable retrieval cost                                            | 1 minute - 12 hours | Long-term archiving with flexible retrieval needs                                                                                                                                                                                         |
| **S3 Glacier Deep Archive**    | ≥3                       | Rarely accessed (1-2 times/year) | Lowest storage cost, high retrieval cost                                                | 12 - 48 hours      | Long-term digital preservation                                                                                                                                                                                                            |
| **S3 Outposts**                | On-premises              | Varies                       | Based on AWS Outposts infrastructure                                                      | Local retrieval    | Compliance with data residency requirements                                                                                                                                                                                                 |

*   **Comparing Amazon EBS and Amazon S3**:

| **Criteria**        | **Amazon S3**                                                              | **Amazon EBS**                                                           |
| :------------------ | :------------------------------------------------------------------------- | :----------------------------------------------------------------------- |
| **Storage Type**    | Object Storage                                                             | Block Storage                                                            |
| **Primary Use Case** | Storing static data like images, documents, videos                         | Storing dynamic data that requires frequent modifications               |
| **Data Access**     | Each file is a separate object; must re-upload the entire file when modified | Updates occur at the block level, only modifying changed parts          |
| **Performance**     | Optimized for high concurrent access, supports public URLs                  | Optimized for high-performance read/write operations, requires EC2     |
| **Durability**      | 11 nines (99.999999999%)                                                   | Depends on snapshots and backups                                       |
| **Cost**            | Lower for long-term storage                                                | Higher due to optimized read/write performance                         |
| **Special Features** | Serverless, does not require EC2, easy web access                           | Requires EC2, supports fast data retrieval                              |

*   **Comparing Amazon EBS and Amazon Elastic File System (EFS)**:

| **Criteria**        | **Amazon EFS**                                                                                                    | **Amazon EBS**                                                           |
| :------------------ | :---------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------- |
| **Storage Type**    | File System                                                                                                       | Block Storage                                                            |
| **Primary Use Case** | A large number of services and resources need to access the same data at the same time.                         | Storing dynamic data that requires frequent modifications               |
| **Durability**      | Stores data in multiple AZs.                                                                                     | Stores data in a single AZ, depends on snapshots and backups            |
| **Special Features** | As you add and remove files, Amazon EFS grows and shrinks automatically. *Additionally, on-premises servers can access Amazon EFS using AWS Direct Connect.* | Cannot automatically grows on demand                                     |

*   **Amazon Relational Database Service(RDS)** : a service that enables you to run relational databases in the AWS Cloud. This service automates tasks such as hardware provisioning, database setup, patching, backups and can connect to other services such as AWS Lambda.

*6 Amazon RDS database engines:*

*   *Amazon Aurora*
*   *PostgreSQL*
*   *MySQL*
*   *MariaDB*
*   *Oracle Database*
*   *Microsoft SQL Server*
*   **Amazon Aurora:** an enterprise-class relational database. It is compatible with MySQL and PostgreSQL relational databases.
    *   It is up to five times faster than standard MySQL databases and up to three times faster than standard PostgreSQL databases.
    *   It replicates six copies of your data across three Availability Zones and continuously backs up data to Amazon S3.
*   **Amazon DynamoDB:** a key-value database service. It delivers single-digit millisecond performance at any scale.
    *   DynamoDB is serverless.
    *   Auto scaling: suitable choice for use cases that require high performance while scaling.
*   **Amazon RDS and Amazon DynamoDB Comparison**:

| **Feature**           | **Amazon RDS (Relational Database)**                                       | **Amazon DynamoDB (Non-Relational Database)**                           |
| :-------------------- | :------------------------------------------------------------------------- | :---------------------------------------------------------------------- |
| **Data Structure**    | Structured, relational                                                     | Key-value and document-based                                            |
| **Use Case**          | Complex queries, business analytics, transactional applications requiring joins | High-speed, scalable lookups, real-time applications, IoT, gaming        |
| **Performance**       | Optimized for complex relationships and transactions                         | Optimized for high-speed, low-latency queries                           |
| **Scaling**           | Vertical scaling                                                             | Horizontal scaling                                                      |
| **Cost**              | Higher cost due to computing resources and relational features              | Lower cost for simple, high-volume operations                         |
| **Example Use Case**  | Sales supply chain management, financial applications                        | Employee directory, real-time user data, leaderboards                    |

*   **Amazon Redshift:** a data warehousing service that you can use for big data analytics. It offers the ability to collect data from many sources and helps you to understand relationships and trends across your data.
*   **AWS Database Migration Service (AWS DMS):** migrate relational databases, nonrelational databases, and other types of data stores.
    *   Development and test database migrations (without affecting production users)
    *   Database consolidation: Combining several databases into a single database.
    *   Continuous replication: Sending ongoing copies of your data to other target sources instead of doing a one-time migration.
*   Additional database services:
    *   Amazon DocumentDB: supports MongoDB workloads.
    *   Amazon Neptune: a graph database service, build and run applications that work with highly connected datasets, such as recommendation engines, fraud detection, and knowledge graphs.
    *   Amazon Quantum Ledger Database (QLDB): review a complete history of all the changes that have been made to your application data. (supply chain, financial records that require 100% immutability)
    *   Amazon Managed Blockchain: create and manage blockchain networks with open-source frameworks.
    *   Amazon ElastiCache: adds caching layers on top of your databases to help improve the read times of common requests. *It supports two types of data stores: Redis and Memcached*.
    *   Amazon DynamoDB Accelerator: an in-memory cache for DynamoDB. It helps improve response times from single-digit milliseconds to microseconds.


