# postgresport
PostgreSQL is an advanced object-relational database management system that supports an extended subset of the SQL standard, including transactions, foreign keys, subqueries, triggers, user-defined types and functions

## Invoking the postgresql database
With the current implementation we can invoke the postgresql database in the following way, execute the commands from the --prefix path
1. Initializing the database cluster
   `$ bin/initdb -D mydb`
2. Change the `io_method` parameter(in file mydb/postgresql.conf) to `sync` from `worker`
3. Execute the postgres command in single user mode
   `$ bin/postgres --single -D tempdb postgres`
4. This is prompt us a interactive terminal to execute SQL commands
```
backend> CREATE TABLE test_table (id INT, name TEXT);
backend> 
backend> INSERT INTO test_table VALUES (1, 'Alice'), (2, 'Bob');
backend> SELECT * FROM test_table
	 1: id	(typeid = 23, len = 4, typmod = -1, byval = t)
	 2: name	(typeid = 25, len = -1, typmod = -1, byval = f)
	----
	 1: id = "1"	(typeid = 23, len = 4, typmod = -1, byval = t)
	 2: name = "Alice"	(typeid = 25, len = -1, typmod = -1, byval = f)
	----
	 1: id = "2"	(typeid = 23, len = 4, typmod = -1, byval = t)
	 2: name = "Bob"	(typeid = 25, len = -1, typmod = -1, byval = f)
	----
backend> SELECT current_database();
	 1: current_database	(typeid = 19, len = 64, typmod = -1, byval = f)
	----
	 1: current_database = "template1"	(typeid = 19, len = 64, typmod = -1, byval = f)
	----
backend> SELECT version();
	 1: version	(typeid = 25, len = -1, typmod = -1, byval = f)
	----
	 1: version = "PostgreSQL 18beta1 on i370-ibm-openedition, compiled by C/C++ for Open Enterprise Languages on z/OS 2.0.0, clang version 14.0.0 (build 985f418), 64-bit"	(typeid = 25, len = -1, typmod = -1, byval = f)
	----
backend> SELECT pg_backend_pid();
	 1: pg_backend_pid	(typeid = 23, len = 4, typmod = -1, byval = t)
	----
	 1: pg_backend_pid = "2160"	(typeid = 23, len = 4, typmod = -1, byval = t)
	----
backend> SHOW work_mem;
	 1: work_mem	(typeid = 25, len = -1, typmod = -1, byval = f)
	----
	 1: work_mem = "4MB"	(typeid = 25, len = -1, typmod = -1, byval = f)
	----
backend> SELECT * FROM non_existent_table;
	 2025-07-23 09:30:04.641 EDT [2160] ERROR:  relation "non_existent_table" does not exist at character 15
	 2025-07-23 09:30:04.641 EDT [2160] STATEMENT:  SELECT * FROM non_existent_table;
```
