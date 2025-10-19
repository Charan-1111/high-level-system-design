# Database Sharding
- Database sharding is a horizontal scaling technique used to split a large database into smaller independent pieces called shards.
- These shards are distributed across multiple servers or nodes, each responsible for handling a specific subset of the data.
- Sharding is widely used by large-scale applications and services, that handle massive amounts of data such as social networks, e-commerce, search engines, gaming.

## Benefits of Sharding
- **Performance Improvement** - By distributing the data across multiple servers, sharding can significantly reduce the load on any single server, resulting in faster query execution and improved overall system performance.
- **Scalability** - Sharding allows databases to grow horizontally. As data volume increases, new shards can be added to spread the load evenly across the cluster.
- **High Availability** - With data spread across multiple shards, the failure of a single shard doesn't bring down the entire system. Other shards can continue serving requests, ensuring high availability.
- **Geographical Distribution** - Sharding allows us to strategically place shards closer to users, reducing latency and improving the user experience.
- **Reduced Cost** - Instead of scaling vertically by investing in more powerful and expensive hardware sharding allows for cost-effective scaling by utilizing commodity hardware.

## Working of Sharding
- Sharding process involves several key components including
1. **Sharding Key** - Sharding key is a unique identifier used to determine which shard a particular piece of data belongs to. It can be a single column or a combination of columns.
2. **Data Partitioning** - Partitioning involves splitting the data into shards based on the shard key. Each shard represents a portion of the total data set. Common strategies to partition database are range-based, hash-based, and directory-based.
3. **Shard Mapping** - Creating a mapping of shard keys to shard locations.
4. **Shard Management** - Shard manager oversees the distribution of data across shards, ensuring data consistency and integrity.
5. **Query Routing** - Query router intercepts incoming queries and directs them to the appropriate shard(s) based on the shard keys.

- [ ] Read about sharding strategies, challenges and best practices.
