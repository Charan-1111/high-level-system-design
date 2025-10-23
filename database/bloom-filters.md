# Bloom Filters
- Bloom Filter is a probabilistic data structure that allows us to quickly check whether an element might be in a set.
- Useful in situations where we need fast lookups and don't want to use large amount of memory, but ok with occasional false positives.

- ## Components of Bloom Filters
	- **Bit Array** - Bloom Filter consists of a bit array of fixed size, initialized to all zeros. This array represents whether certain elements are in the set.
	- **Hash Function** - To add or check an element a Bloom filter uses multiple hash functions. Each hash function maps an element to an index in the bit array.

- ## Working of Bloom Filter
	- Bloom filter works by using multiple hash functions to map each element in the set to a bit array.
	1. **Initialization**
		- Bloom Filter starts with an empty bit array of size m ( all bits set to 0 initially ).
		- It also requires k independent hash functions, each of which maps an element to one of the m positions in the bit array.

	2. **Inserting an Element**
		- To insert an element into the Bloom filter, we pass it through each of the k hash functions to get k positions in the bit array.
		- The bits at this positions are set to 1.

	3. **Checking for Membership**
		- To check if an element is in the set, again pass it through k hash functions to get k positions.
		- If all the bits at these positions are set to 1, the element is considered to be in the set ( though there is a chance that it might be a false positive ).
		- If any of the bit at these positions is 0, the the element is definitely not in the set.


- [ ] Read about the use cases, advantages, disadvantages of bloom filters
