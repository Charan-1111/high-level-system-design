# Parallelism
- Parallelism means multiple tasks are getting executed simultaneously.
- To achieve parallelism, an application divides its tasks into smaller independent subtasks.
- These subtasks are distributed across multiple CPUs, CPU cores, GPU cores or similar processing units allowing them to be processes in parallel.
- To achieve true parallelism, the application must
	- use more than one thread.
	- ensure each thread is assigned to a separate CPU core or processing unit

- ## Working of Parallelism
	- Modern CPUs consists of multiple cores. Each core can independently execute a task
	1. **Task Division** - The problem is broken into smaller independent sub-tasks.
	2. **Task Assignment** - Sub-tasks are distributed across multiple CPU cores.
	3. **Execution** - Each core processes its assigned task simultaneously.
	4. **Result Aggregation** - Results from all cores are combined to form the final output.
