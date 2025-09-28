# ACID Transactions.
- A -> Atomicity
- C -> Consistency
- I -> Isolation
- D -> Durability
## Database Transaction
- In the context of database, a transaction means a squence of one/more operations ( such as inserts, updates, or deletes) that database treats as single action.
- A transaction is either fully succeeds or fully fails, with no in-between states.
- Without transactions, databases could end up in inconsistent states.
- Transactions solve the inconsistency problem for the database by enforcing rules like ACID properties.


1. ## Atomicity
	- Atomicity ensures that a transaction comprising multiple operations, executes as a single and indivisible unit of work.
	- It makes sure that a transaction is either fully succeeds ( commits ) or fully fails ( rolls back ).
	- If any part of the transaction fails, the entire transaction is rolled back and the database is restored to the state it was in before the transaction began.
	- Automicity abstracts away the complexity of manually undoing the changes if somethins goes wrong.
	- ### How databases implelemts Atomicity
		- Database uses two key mechanisms to implement Automicity.
			1. **Transaction Logs ( Write-Ahead Logs )**
				- Every operation is recorded in a write-ahead log before it is applied to the actual database tables.
				- If a failure occurs, database uses this logs to undo the incomplete changes.
        
           2. **Commit / Rollback Protocols**
		           - Database provides commands like *BEGIN TRANSACTION*, *COMMIT* and *ROLLBACK*.
		           - Any changes made in between *BEGIN TRANSACTION* and *COMMIT* are considered as in-progress and won't directly and permanently applied unless the transaction commits successfully.
		           - If any step fail, or if the *ROLLBACK* is issued explicitly, all changes since start of the transaction will be undone. 

2. ## Consistency
	- Consistency ensures that any transaction will bring the database from one valid state to another valid state - never leaving it in a broken or invalid state.
	- It means that all the data integrity constrains like **primary key** ( no duplicate ID ), **foreign key** ( related records must exist in parent tables ) and **check** constrains are satisfied before and after transaction.
	- If a transaction tries to violates these rules it will not be commited, and the database will revert to its previous state.
	- ### How to implement Consistency
		1. **Database schema constrains**
			- NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK constraints and other schema definations ensure no invalid entries are allowed.
		2. **Triggers and Stored Procedures**
			- Triggers can automatically check additional rules whenever rows are inserted, updated or deleted.
			- Stored procedures can contain logic to validate data before commiting.
		3. **Application-level Safeguards**
			- While the database enforces constrains at lower level, applications often adds extra checks, like ensuring bussiness rules are followed or data is validated before it even reaches the database layer.

3. ## Isolation
	- Isolation ensures that concurrently running transactions do not interfere with each other's intermediate states.
	- While a transaction is in progress, it updates remains invisible to other ongoing transactions - givnig the illusion that each transaction running sequentially at a time.
	- Without isolation, two or more transactions could read and write partial or uncommitted data from each other, causing incorrect or inconsistent results.
	- ### Concurrency Anomolies
		1. **Dirty Read**
			- Transaction A reads data that Transaction B has modified but not committed yet.
			- If Transaction B rolls back later, Transaction A endsup holding an invalid or dirty value, that never truly existed in the committed state.
		2. **Non-Repeatable Read**
			- Transaction A reads the same row(s) multiple times during its execution but sees different data because another transaction updated or deleted those rows in between A's reads.
		3. **Phantom Read**
			- Transaction A performs a query that returns a set of rows, Another transaction inserts, updates or deletes rows that match A's query conditions.
			- If A re-runs the same query, it sees a different set of rows  ( Phantoms ).
	- ### Isolation Levels
		- Databases typically allows us to choose the level of isolation, which balances data correctness with performance.
		- Higher isolation level provides stronger data consistency, but can reduce systems performance by increasing the wait time for transactions.
		- There are four. common isolation levels.
			1. **Read Uncommitted**
				- Allows ditry reads : transactions can see uncommitted changes.
				- Rarely used as it can leads to sever anomolies.
			2. **Read Committed**
				- A transaction only sees the data that has been committed only at the momemt of reading.
				- Preventing ditry reads, but non-repeatable reads and phantom reads can still occur.
			3. **Repeatable Reads**
				- Ensures if reading the same rows multiple times within a transaction, we will get the same values ( unless we explicitly modify the data ).
				- Prevents ditry reads and non-repeatable reads, but phantom reads may still happen ( depending on the database engine ).
			4. **Serialize**
				- The heighest level of isolation, action as if all transactions happen sequentially one at a time.
				- Prevents dirty reads, non-repeatable reads and phantom reads.
				- Most expensive in terms of performace and concurrency because it can require more lockings and more conflict checks.
	- ### How to enforce Isolation in Database
		1. **Locking**
			- **Pessimistic Concurrency Control**
				- Rows or tables are locked so that no other transaction can read or write them until the lock is released.
				- Can lead to blocking or deadlocks if multiple transactions compete for the same locks.
		2. **MVCC ( Multi-Version Concurrency Control )**
			- **Optimistic Concurrency Control**
				- Instead of blocking the reads, the database keeps multiple versions of a row.
				- Readers see a consistent snapshot of data ( like a point-in-time view ), while writers create a new version of the row when updating.
				- This approach reduces lock contention but requires carefully managing row versions and cleanup.
		3. **Snapshot Isolation**
			- A form of MVCC where each transaction sees data as it was at the start ( or a consistent point ) of the transaction.
			- Prevents non-repeatable reads and ditry reads. Phantom reads may still occur unless the isolation level is fully serializable.

4. ## Durability
	- Durability ensures that once a transaction has been committed, the changes it made will survive, even in the face of power failures, crashes or other catastrophic events.
	- In other words, once a transaction says done, the data is permanantly recorded and cannot simply disappear.
	- ### How Databases Ensures Durability
		1. **Transactions Logs ( Write-Ahead Logging )**
			- Most relational databases rely on a write-ahead logging ( WAL ) to preserve changes before they are written to the main data file.
				1. **Write changes to WAL** :- The intended operations ( updates, inserts, deletes ) recorded, in the WAL on durable storage ( disk ).
				2. **Commit the Transaction** :- Once the WAL entry is persisted, the database can mark the transaction as committed.
				3. **Apply changes to Main Data Files** :- The updated data eventually gets written to the main files - possibly first in memory, then flushed to disk.
			- If database crashed, it uses WAL during the recovery.
				- **Redo** :- Any committed transactions not yet reflected in the main file are reapplied.
				- **Undo** :- Any incomplete ( uncommitted ) transactions are rolled back to keep the database consistent.
				
		2. **Replication / Redundancy**
			- In addition to WAL, many systems use replication to ensure data remains durable even if hardware or entire data center fails.
			- **Synchronous Replication** :- Writes are immediatelu copied to multiple nodes or data centers. A transaction is marked committed only if the primary and atleast one of the replica confirm it's safely stored.
			- **Asynchronous Replication** :- Changes eventually sync to other nodes but there is a ( small ) window where data loss can occur if the primary fails before the replica is updated.
		
		3. **Backups**
			- Regular backups provide a safety net beyond logs and replication. In case of severe corruption, human error or catastrophic failures.
			- **Full Backups** :- Capture the entire database at a point in time.
			- **Incremental / Differential Backups** :- Store changes since the last backup for faster, more frequent backups.
			- **Off-site Storage** :- Ensures backups remain safe from localized disaster, allowing us to restore data even if hardware is damaged.
			
