# Rate Limiting
- Rate limiting is a technique using in computer systems, especially APIs, Servers or web applications to control the number of requests a client can make in a specific time period.
- It ensures
	- Fair usage of  resources.
	- System stability and performace.
	- Protection against abuse, spam or DoS ( Denial of Service ) attacks.
- Working:
	- Every User/IP address is assigned a request quota ( eg 100 req / min )
	- If they exceed that limit, server blocks additional requests temporarily and returns an error ( HTTP 429 )
- There are 5 common rate limiting algorithms.
		1. Token Bucket
		2. Leaky Bucket
		3. Fixed Window Counter
		4. Sliding Window Log
		5. Sliding Window Counter

1. ## Token Bucket
	- Token Bucket algorihm is one of the most popular and widely used rate limiting appraoches due to its simplicity and effectiveness.
	- **Working**:
		- Imagine a bucket that holds tokens.
		- The bucket has a maximum capacity of tokens.
		- Tokens are added to the bucket at a fixed rate ( eg : 10 tokens / requests )
		- When a request arrives, it must obtain a token from the bucket to proceed.
		- If there are enough tokens, the request is allowed and tokens are removed.
		- If there aren't enough tokens the requests are dropped.
	- **Pros**
		- Relatively straight forward to implement.
		- Allows bursts of requests up to the bucket capacity, accomodating short-term spikes.	
	- **Cons**
		- Memory usage scales with the number of users if implemented per-user.
		- It does not guarantee a perfectly smooth rate of requests.
- [ ] Add the implementation for the token bucket rate limiting in golang


2. ## Leaky Bucket
	- The Leaky Bucket algorithm is similar to token bucket, but focuses on smoothign out bursty traffic.
	- **Working**
		- Imagine a bucket with a small hole at the bottom.
		- Requests enter the bucket from the top.
		- The bucket proccesses ( "Leaks" ) requests at a constant rate through the hole.
		- If bucket is full new requests are discarded.
	- **Pros**
		- Proccesses requests at a stready rate, preventing sudden bursts from overwhelming the system.
		- Provides a consistent and predictable rate of processing requests.
	- **Cons**
		- Does not handle sudden bursts of requests well, excess requests are immediately dropped.
		- Slightly more complex than token bucket.
	- [ ] Implement algorithm in golang
