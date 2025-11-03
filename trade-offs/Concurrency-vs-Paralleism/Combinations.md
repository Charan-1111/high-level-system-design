# Combinations of Concurrency and Parallelism
- ## Concurrent, not Parallel
	- An application can be concurrent, without being parallel.
	- Application makes progress on multiple tasks at the same time concurrently.
	- However, it achieves this by switching between tasks rapidly, rather than running them simultaneously.
	- Eg :- A single-core CPU alternating between tasks, giving the illusion of multitasking.

- ## Parallel, Not Concurrent
	- An application can be parallel, without being concurrent.
	- A single task is divided into multiple subtasks and these tasks are executed separately on separate cores.
	- There is not overlap between tasks; one task ( and its subtasks ) completes before the next task starts.
	- Eg :- Video rendering, where a single video is divided into multiple frames, and each frame is processed parallel.

- ## Neither Concurrent, Nor Parallel.
	- An application cam be neither concurrent , nor parallel.
	- Tasks are executed sequentially. one at a time, without any overlap or parallel execution.
	- Eg :- A single-core CPU where only one task is processed, and it completes fully before the next task begins.

- ## Concurrent and Parallel
	- An application can be both concurrent and parallel, combining the strengths of both execution models.
	- Multiple tasks makes progress at the same time and each task is also divided into subtasks that are executed in parallel.
	- Eg :- A multi-core CPU, where some subtasks are running concurrently on the same core, while others run parallel on separate cores
