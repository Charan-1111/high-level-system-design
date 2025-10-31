# Concurrency
- Concurrency means multiple tasks making progress at the same time, not necessarily executing simultaneously but begin in progress together.
- In computers, the tasks are executed by CPU. A single CPU can work on only one task at a time, it achieves concurrency by rapidly switching between tasks.
- Concurrency is primarily achieved using threads, which are smallest units of execution within a process.
- CPU switches between threads to handle multiple tasks concurrently, ensuring the system remains responsive.
- Primary objective of concurrency is to maximize the CPU utilization by minimizing the CPU idle time.

- ## Building blocks of Concurrency
	1. **Threads**
		- A thread is the smallest unit of execution
		- Each thread can execute a sequence of instructions independently.
		- But threads are expensive to create and manage ( especially thousands ). They also causes synchronization issues ( race conditions, deadlocks)
	2. **Processes**
		- A process has its own memory space and resources.
		- Multiple processes can run concurrently, isolated from each other.
		- Pros :- Fault Isolation
		- Cons :- Heavy weight communication.
	3. **Coroutines/Goroutines**
		- Light weight, cooperative threads that are scheduled by the language runtime instead of the OS.
		- They are very cheap to create, can spawn thousands.
	4. **Event loop/Async Model**
		- Single threaded systems ( like Node.js or python asyncio ) use an event loop to handle multiple I/O-bound tasks concurrently using callbacks or coroutines.
	5. **Synchronization Mechanisms**
		- Concurrency introduces shared resource issues.
		- We need to use coordination tools like
			- Mutex
			-  Semaphore
			- Monitor
			- Channel/Queue
			- Atomic Operations

- ## Working of Concurrency
	- Concurrency in CPU is achieved through context switching
	- **Context Saving** - When the CPU switches from one task to another, it saves the current task state in memory ( eg :- program counter, registers ).
	- **Context Loading**- CPU then loads the context of the next task and continues executing it.
	- **Rapid Switching** - CPU repeats this process, switching between tasks so quickly that it seems like they are running simultaneously.

- ## Cost of Context Switching
	- While context switching enables concurrency, it also introduces overhead.
	- Every switch requires sabing and restoring tasks states, which consumes both time and resources.
	- Excessive context switching can degrade performance by increasing CPU overhead.

- ## Benefits of Concurrency
	- Better resource utilization
	- Responsive Systems
	- Handles I/O-tasks efficiently.
	- Scalable architectures.

- ## Challenges of Concurrency
	- Harder debugging
	- Race conditions
	- Synchronization overhead
	- Testing complexity.

- ## Concurrency in Distributed Systems
	- Concurrency extends beyond threads to nodes
		- Multiple microservices handle requests concurrently.
		- Consensus algorithms (like Raft) use concurrent message passing.
		- Distributed locks ensure safe coordination across nodes.
