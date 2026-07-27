<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Load Data into DynamoDB

**Project Link:** [View Project](http://nextwork.ai/projects/aws-databases-dynamodb)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Load Data into a DynamoDB Table

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-dynamodb_b481c730)

---

## Introducing Today's Project!

### What is Amazon DynamoDB?

Amazon DynamoDB is a fully managed, serverless NoSQL database service that organizes data using flexible, schema-less tables. It is incredibly useful because it delivers rapid, single-digit millisecond performance at any scale, automatically handling data partitioning and replication to ensure high availability and consistent speed without the administrative burden of managing physical database servers.

### How I used Amazon DynamoDB in this project

In today's project, I used Amazon DynamoDB to store and manage our community's platform data within a highly scalable NoSQL database. I provisioned tables manually via the console and automated the creation of additional tables using the AWS CLI inside AWS CloudShell. Finally, I loaded datasets using batch commands and edited individual items directly to demonstrate how DynamoDB's flexible, schema-less structure easily accommodates diverse data models without rigid constraints.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is how seamless and fast it would be to interact with and create tables using AWS CloudShell and the AWS CLI. I was surprised that we could run automated commands to provision multiple Amazon DynamoDB tables simultaneously, rather than manually setting up each resource one-by-one in the AWS Management Console. Seeing the data files load instantly via the command line really highlighted how powerful scripting is for managing database infrastructure.

### This project took me...

This project took me approximately 1 hour of focused effort to complete. During this time, I was able to successfully provision an Amazon DynamoDB table manually, automate the creation of multiple other tables using the AWS CLI inside AWS CloudShell, and batch-write catalog records to compare relational versus non-relational database structures.

---

## Create a DynamoDB table

DynamoDB tables organize data using items and attributes instead of the traditional rows and columns found in relational databases. An item represents a single, unique record in the table, while attributes represent the individual details or properties belonging to that item. Combined with a partition key to group and retrieve data, this structure allows Amazon DynamoDB to store highly flexible, schemaless data that can be queried with extreme speed.

An attribute is a fundamental data element in Amazon DynamoDB that represents a specific piece of information or property stored within an item. Unlike traditional columns in a relational database which force every single row to conform to the exact same structure, attributes in DynamoDB do not require a rigid, table-wide schema, meaning each individual item can have its own completely unique set of properties to provide maximum storage flexibility.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-dynamodb_a3cefee0)

---

## Read and Write Capacity

Read capacity units (RCUs) and write capacity units (WCUs) are the metrics used to measure and allocate processing throughput for an Amazon DynamoDB table. One RCU provides the capacity to perform up to two read requests per second, while one WCU provides the capacity for one write request per second, functioning as the performance engines of your database.

Amazon DynamoDB's Free Tier covers up to 25 GB of storage alongside 25 read capacity units and 25 write capacity units, which is enough to handle 200 million requests per month for free. I turned off auto scaling because if the table experiences a sudden burst of activity or a large data update, an unmonitored auto scaling policy can automatically scale up our throughput settings beyond these free limits, which could lead to unwanted charges on our AWS account.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-dynamodb_ef47dd8f)

---

## Using CLI and CloudShell

AWS CloudShell is a browser-based, pre-authenticated terminal shell accessible directly from the AWS Management Console that allows you to run commands and manage cloud resources securely. Because it comes with the AWS CLI pre-installed and automatically inherits your active console login permissions, it enables you to quickly deploy infrastructure and run automation scripts without needing to configure security credentials or install software on your local machine.

AWS CLI is a command-line tool that lets you provision, manage, and automate AWS resources directly from your terminal using text-based commands instead of clicking through the AWS Management Console. By allowing engineers to script deployments and interact directly with cloud services like Amazon DynamoDB, the AWS CLI provides the speed, repeatability, and precision required for professional cloud operations and DevOps pipelines.

I ran a CLI command in AWS CloudShell that created four new Amazon DynamoDB tables named ContentCatalog, Forum, Post, and Comment. This automated script allowed me to simultaneously define their schema structures—including partition keys and sort keys—and provision their initial read and write throughput settings in seconds instead of clicking through the AWS Management Console for each individual table.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-dynamodb_81e0258b)

---

## Loading Data with CLI

I ran a CLI command in AWS CloudShell that created four new Amazon DynamoDB tables named ContentCatalog, Forum, Post, and Comment by executing the aws dynamodb create-table command. This command allowed me to automatically establish our table structures by defining key attributes, setting partition keys and sort keys, and establishing an initial throughput capacity of 1 read and 1 write capacity unit for each resource in a single run.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-dynamodb_791c600b)

---

## Observing Item Attributes

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-dynamodb_b481c731)

I checked a ContentCatalog item, which had the following attributes: Id, Title, ContentType, Difficulty, ProjectCategory, and Services. These key-value attributes represent the metadata of our project catalog item, demonstrating how Amazon DynamoDB organizes flexible records using unique properties rather than forcing a uniform structure on all entries.

I checked another ContentCatalog item, which had a different set of attributes, specifically lacking the Difficulty, ProjectCategory, and newly added StudentsComplete fields. This video item only maintained properties relevant to its own media format, demonstrating that Amazon DynamoDB uses a schema-less structure where individual items do not force their properties onto other records in the same table.

---

## Benefits of DynamoDB

A benefit of DynamoDB over relational databases is flexibility, because Amazon DynamoDB is a schema-less database where individual items in the same table can have completely different attributes. Unlike a relational database that forces every single row to conform to a rigid, pre-defined column structure, DynamoDB lets you store unique properties for each record on the fly, making it perfect for handling rapidly changing or diverse datasets without requiring database-wide schema migrations.

Another benefit over relational databases is speed, because Amazon DynamoDB uses a partition key to partition and index data, allowing it to locate specific records directly. Unlike a relational database which often has to perform resource-heavy operations like table joins or full table scans as datasets grow, DynamoDB maintains consistent, single-digit millisecond latency at any scale by routing queries directly to the storage partition holding the requested items.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-dynamodb_b481c730)

---

---
