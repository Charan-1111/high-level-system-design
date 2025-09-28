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
