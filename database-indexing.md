# Database Indexing
- A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional space and write overhead.
- Without indexing db query performs full table scan ( means scans through every row ), which is time consuming. With indexing, database lookup is much faster using the index ( avoids scanning the entire table ).
- ## Working of Database Indexing
	1. **Index Creation** :- Database administrator creates index on a specific column or set of columns.
	2. **Index Building** :- DBMS builds the index by scanning the table and storing the values of indexed column(s) along with a pointer to the corresponding data.
	3. **Query Execution** :- When a query is executed, the database engine checks if an index exists for the requested column(s).
	4. **Index Search** :- If an index exists, the database searches the index for the requested data, using the pointers to quickly locate the data.
	5. **Data Retrieval** :- Database retrieves the requested data, using the pointers from the index.

- ## Benefits of Database Indexing
	- **Faster Query Performance** - Indexes can significantly improves query performance ( especially for large datasets ) by reducing the amount of data that needed to be scanned.
	- **Reduced CPU Usage** - By reducing the number of rows that need to be scanned, indexes can decrease CPU usage and optimize resource utilization.
	- **Rapid Data Retrieval** - Indexes enable quick data retrieval for queries that involves equality or range conditions on the indexed columns.
	- **Efficient Sorting** - Indexes can also be used to efficiently sort the data based on the indexed columns, eliminating the need for expensive sorting operations.
	- **Better Data Organization** - Indexes can help maintain data organization and structure, making it easier to manage and maintain the database.

- ## Types of Database Indexes
	- **Indexes based on Structure and Key Attributes**
		1. **Primary Index** - Automatically created when a primary key constraint is defined on a table. It ensures uniqueness and helps with superfast lookups using the primary key.
		2. **Clustered Index** - Determines the order in which data is physically stored in the table. A clustered index is most useful when we aer searching in a range. Only one clustered index can exist per table.
		3. **Non-Clustered or Secondary Index** - This index does not store data in the order of the index. Instead it provides a list of virtual pointers or references to the location where the data is actually stored.
