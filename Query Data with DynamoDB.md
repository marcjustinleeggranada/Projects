<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Query Data with DynamoDB

**Project Link:** [View Project](http://nextwork.ai/projects/aws-databases-query)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Query Data with DynamoDB

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-query_733d9399)

---

## Introducing Today's Project!

### What is Amazon DynamoDB?

Amazon DynamoDB is a fully managed, serverless NoSQL database service from AWS that delivers fast, predictable performance with seamless, automatic scaling. It is highly useful because it provides consistent single-digit millisecond response times at any scale, handles data partitioning automatically, and offers a flexible schema design where items in the same table can have different attributes. This design eliminates the operational overhead of managing physical database servers while guaranteeing high availability and security, making it ideal for high-throughput applications like mobile apps, gaming, and real-time data ingestion.

### How I used Amazon DynamoDB in this project

In today's project, I used Amazon DynamoDB to run targeted search queries through both the AWS Management Console and the AWS CLI inside AWS CloudShell. By leveraging partition keys and sort keys, I learned to isolate specific data points, analyzed how strongly consistent reads impact consumed capacity compared to eventual consistency, and executed an atomic database transaction using transact-write-items to synchronously update related records across my Comment and Forum tables.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is how straightforward it is to perform a multi-table database transaction using transact-write-items in the AWS CLI. I assumed that coordinating updates across different tables in Amazon DynamoDB would require complex, manual backend scripting, but executing the single atomic transaction instantly synchronized our Comment and Forum tables while protecting our database from partial update failures.

### This project took me...

This project took me approximately 1 hour to complete. A majority of my time was spent executing and analyzing programmatic read operations via the AWS CLI in AWS CloudShell, as well as designing the JSON structure for the transact-write-items transaction to safely synchronize updates across both the Comment and Forum tables in Amazon DynamoDB.

---

## Querying DynamoDB Tables

A partition key is a fundamental attribute in Amazon DynamoDB that determines how data is physically stored and distributed across servers. It acts as the input to an internal hash function, allowing the database to instantly locate and retrieve specific items with single-digit millisecond latency, which makes it highly efficient and scalable compared to scanning an entire database table.

A sort key is a secondary attribute in Amazon DynamoDB used alongside a partition key to create a composite primary key. While the partition key routes your query to the correct physical storage partition, the sort key organizes all items sharing that partition key in sorted order. This setup allows you to run high-performance range queries—using conditions like "greater than" or "begins with"—to retrieve a subset of related records rapidly without resorting to inefficient, full-table scans.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-query_d105b0b0)

---

## Limits of Using DynamoDB

I ran into an error when I queried for all comments posted by User Abdulrahman. This was because Amazon DynamoDB requires you to specify the partition key in a query operation to find where the data is stored. Because the author's name is a non-key attribute rather than the table's partition key, the AWS Management Console threw an error, showing why upfront data modeling is essential before uploading data.

Insights we could extract from our Comment table includes the total number of responses written for a specific community post, sorted dynamically by their timestamp using the sort key. Conversely, insights we can't easily extract from the Comment table includes a consolidated list of every comment written by a specific author, because the author name is a non-key attribute that cannot be queried directly without running an expensive table scan.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-query_cb3e260c)

---

## Running Queries with CLI

A query I ran in CloudShell was aws dynamodb get-item --table-name ContentCatalog --key '{"Id":{"N":"202"}}' --projection-expression "Title, ContentType, Services" --return-consumed-capacity TOTAL. This query will retrieve a single item with the numeric ID 202 from the ContentCatalog table, returning only the requested Title, ContentType, and Services attributes while displaying the total read capacity units consumed by the read operation to help monitor performance in Amazon DynamoDB.

Query options I could add to my query are --consistent-read to request a strongly consistent read that guarantees the most up-to-date data, --projection-expression to isolate and retrieve only specific attributes rather than the entire item, and --return-consumed-capacity to output the total read capacity units utilized by the request in Amazon DynamoDB.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-query_733d9399)

---

## Transactions

A database transaction is a group of multiple database operations that are treated as a single, logical unit of work, executing under an "all-or-nothing" rule. In Amazon DynamoDB, using programmatic options like transact-write-items ensures that either all updates succeed or none of them are applied, which prevents partial updates and keeps related tables perfectly synchronized across your entire environment.

I ran a transaction using the AWS CLI command aws dynamodb transact-write-items. This transaction did two things simultaneously: first, it added a new comment record for User Connor into the Comment table with all of its attributes, and second, it automatically incremented the Comments counter by 1 for the "Events" item in the related Forum table, ensuring our connected data remains perfectly synchronized across Amazon DynamoDB.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-databases-query_2f65f83e)

---

---
