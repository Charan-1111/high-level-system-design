# Consistent Hashing
- In a distributed systems where node ( servers ) are frequently added or removed, efficiently routing requests becomes challenging.
- A common approach is to hash the request and assign it to server using ***Hash(Key) mod N***, where N is the number of servers.
- But this method is dependent on the number of severs, if there is any change in N, then it can lead to significant rehasing, causing a major redistribution of keys ( requests ).
- Consistent hashing addresses this issue by ensuring that only a small subset of keys need to be reassigned when nodes are added or removed.
