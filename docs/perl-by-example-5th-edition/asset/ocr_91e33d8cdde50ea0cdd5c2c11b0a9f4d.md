# EXERCISE 15
Practicing Queries and Using DBI

# Part 1: SQL Lab—Using the northwind Database

1. Load the northwind database from a script. The northwind database is a good sample database used with Microsoft's Access Database but tailored to work with MySQL as well. You will be provided with the northwind.sql script for this exercise (on CD), a file containing SQL statements to create and populate the northwind database. The file must be located on the client host where you are running mysql.

2. To run the script, go to your MySQL console window and type

```
source c:\document\northwind.sql
```

(Notice that there are no quotes around the name of the file and that absolute or relative pathnames can be used.)

Ways to source the SQL script:

```
mysql> SOURCE C:\path\northwind.sql;
mysql> SOURCE ../path\northwind.sql;
shell> mysql db_name < input_file
```

As the script executes, the results will be displayed on your screen, most of them SQL insert statements. If an error occurs, the process will be aborted, and nothing done.

# Part 2—Practice SQL Commands

+   1. After running the northwind.sql script, start by typing use northwind.

+   2. Type the following SQL commands and explain what they do.

+   a. SHOW DATABASES;

+   b. SHOW TABLES FROM NORTHWIND;

+   c. SHOW FIELDS FROM SHIPPERS;

+   d. DESCRIBE SHIPPERS;

+   3. Use the SQL tutorial, if you need it, to do the following:

+   a. Select all rows from the Shippers table and display the fields.

+   b. Select all rows from the Employees table and display only the FirstName and LastName fields.

+   c. Select the CompanyName and Phone from the Customers table only if the Country is Italy.

+   d. Print in sorted order the ContactName and Country from the Customers table. Sort by Country.