# Database Scaling
- As the user base increases, we cannot store all the data in a single database. If the database is not scaled to handle the load, it can slow down the app and causes problems.
- Below are the strategies to scale the databases.

## 1. Vertical Scaling
- Vertical scaling involves add more resources ( RAM, CPU, storage ) to a single database server.
- It is a easy and quick solution if we have smaller database, but it has its own limitations.
	- It can become expensive, and there is a limit on how much we can scale up.
	- Additionally vertical scaling also introduces single point of failure.

## 2. Indexing
- Database indexes helps us find the data much faster without scanning every single row in the table.
- Indexes are usually created on most frequently queries columns to make read requests faster.
	- But over-indexing can slow down the write performance due to over head.

## 3. Sharding
- A single machine cannot hold so much data, eventually it will ran into out of space and slows down.
- To avoid this, we can split the data into smaller pieces ( shards ), and store them on different servers ( Database Sharding ).
- Distributing data in this manner makes it easier to scale and handle more users.

## 4. Vertical Partitioning
- If some columns are accessed more often than others, it is good to split the database table into smaller tables, each containing a subset of the columns from the original table.
- This helps reduce the amount of data read during queries and can improve performance for specific access patterns.

## 5. Caching
- We can store frequently accessed data in a faster storage layer ( cache ) to speed up access and reduce the load on the database.

## 6. Replication
- If the database servers are located in only one region, users from other regions may face higher latencies.
- To mitigate this, we can replicate the primary database to other regions and handle read requests locally ( Database Replication ).
- With database replication, we can improve read performance, ensure high availability and disaster recovery.
- These replicas are syncronized with the original database ( primary database ), ensuring data consistency.
- Types of Replication
	1. **Synchronous Replication**
		- Changes made to primary database are immediately replicated to all replicas, before the transaction is considered complete.
		- This ensures strong data consistency but can impact performance due to additional overhead.
	2. **Asynchronous Replication**
		- Changes to the primary database are replicated to all replicas with slight delay.
		- This offers better performance but with trade-off of potential data inconsistency between the primary and replicas ( known as replication log ).

## 7. Materialized Views
- Some database queries are complex and can take a long time to run. This can slow down the performance of the application if these queries are run very often.
- Materialized views are per-computed, disk-stored result sets of complex queries.
- Unlike regular views, which are virtual and computed on-the-fly, materialized views physically store the results, making them readily available for fast retrival.
- It significantly improves the query performance for complex and resource-intensive operations.

## 8. Data Denormalization
- Some database queries may involve multiple tables and complex joins.
- These queries are often slow and can make the application slower for larger tables.
- To avoid this, we can add redundancy by combining multiple tables into one to reduce the need for complex joins ( Data Denormalization )
