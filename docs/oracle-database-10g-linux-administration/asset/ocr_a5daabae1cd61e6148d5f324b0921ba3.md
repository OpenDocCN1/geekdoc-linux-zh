backup and recovery, the shared server processes, memory for the XA interface, and memory for parallel message queues for the parallel query option.

The Shared Pool is very important, since an insufficient amount of memory allocated to the Shared Pool can cause performance degradation. The Shared Pool is made up of both the Library Cache and the Data Dictionary Cache.

**The Library Cache**	The Library Cache is used to store shared SQL. Here is cached the parse tree, and the execution plan for every unique SQL statement. If multiple applications issue the same SQL statement, the shared SQL area can be accessed by each of them to reduce the amount of memory needed and to reduce the processing time used for parsing and execution planning.

**The Data Dictionary Cache**	The Oracle Data Dictionary contains a set of tables and views Oracle uses as a reference to the database. Oracle stores information here about both the logical and physical structure of the database. The Data Dictionary contains information like the following:

+   - User information such as user privileges
+   - Integrity constraints defined for tables in the database
+   - Names and data types of all columns in database tables
+   - Information on space allocated and used for schema objects

The Data Dictionary is frequently accessed by Oracle itself for the parsing of SQL statements. This access is essential to the operation of Oracle since performance bottlenecks in the Data Dictionary affect all Oracle users. By making sure that you have allocated a sufficient amount of memory to the Shared Pool, you should see no performance problems.

# ## User Processes

In addition to the Oracle background processes, there are processes that are created on behalf of the user. These are known as the server processes. It is this server process that is responsible for retrieving data requested by the user and returning it to them. In addition, the server process is responsible for modifying data in the buffer cache on behalf of the user.

User, or client, processes are the user’s connections into the Oracle Database server. The user process manipulates the user’s input and communicates with the Oracle server process through the Oracle program interface. The user process is also used to display the information requested by the user and, if necessary, can process this information into a more useful form.