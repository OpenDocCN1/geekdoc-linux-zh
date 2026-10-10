# ## Database Services

Databases are large files that store important information in the form of tables. A table organizes information into a list. Within the list, the set of information about a particular item is called a record. For example, in a list of customer mailing addresses, a single record would contain a customer's first name, last name, street address, city, state, and Zip code. The various categories of information within a record are called fields. For example, in our customer mailing address example, one field contains the city information, one contains the state information, and so on.

Most databases consist of dozens or hundreds of tables that store information used by applications. For example, accounting software typically stores financial data within a database. In large databases, information within certain tables can be related to information within other tables in the same database. These databases are called relational databases, and the tables within are usually linked by a common field. Figure 13-8 shows a simple relational database that consists of two tables with a related EmployeeID field.

Structured Query Language (SQL) is a special programming language used to store and access the data in databases. The database server programs that allow users to access and update the data stored within a database are called SQL servers. Table 13-5 lists common SQL statements that are used to manipulate data on SQL servers.

![](bbox=[0.13, 0.45, 0.88, 0.93])

**Figure 13-8**  A simple relational database structure