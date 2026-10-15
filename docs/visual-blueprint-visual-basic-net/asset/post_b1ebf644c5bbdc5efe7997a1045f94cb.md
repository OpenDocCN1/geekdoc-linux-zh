
# AN INTRODUCTION TO DATABASES

One of the most-used functions in the Visual Basic language's history, powerful database support, provides many functions to automate the development of database applications. You can use databases to quickly and efficiently store large or small quantities of information of any type, as well as search, filter, and manipulate that data to suit your needs. In certain cases where you need to store only a small list of data, you can use text files to more easily store the information. For more information on reading and writing to text files, see Chapter 5.

Visual Basic .NET and other Microsoft languages use a database system called ADO.NET, ADO, or Active Data Objects, allows you to wrap a set of standard functionality around any supported database format. For more information on the concepts of ADO.NET, see the section "An Introduction to ADO.NET."

## DATABASE SOFTWARE

A variety of programs allow you to create database files, and ADO supports most database formats. Common database packages to use with Visual Basic .NET include Microsoft Access, Microsoft SQL, and Oracle. Make sure the vendor of your database provides a native .NET data provider, or an OLEDB compatible provider. ADO.NET can work with databases that support one of these two providers.

Microsoft Access is best suited for creating small databases that do not need to function under a heavy load. Microsoft SQL Server provides a more powerful database solution for large and high-load applications, such as Web development.

## DATABASE STRUCTURE

A database consists of one or more tables, and a table contains one or more records. Each record can have one or more fields that make up its data. Each field in the record contains a single piece of information about that record, such as a string, a number, or a date. For example, you can define a table in a database to store customer information. The table has a field for the customer's first name, last name, address, and phone number. Then you can define individual customers by adding new records to the table.

Database design is a very important part of creating an efficient, powerful, and maintainable application. You should carefully evaluate your data storage needs and create a database that fits those needs while providing flexibility for expansion.

For ADO.NET to access a variety of data sources, it must have a common language that works with a variety of databases. You use Structured Query Language (SQL) to communicate with databases of any format. SQL provides a simple English-like instruction set that can accomplish any action a database supports.

## SQL FEATURES

IBM originally developed SQL in a prototype relational database management system, System R, in the mid 1970s. In 1979, Oracle Corporation introduced the first commercially available implementation of SQL. Since then, the entire database industry has adopted SQL to access their databases. With the help of ADO.NET's ability to support different databases seamlessly, SQL enables you to move between different databases with few changes. For example, you can use Microsoft Access to develop your application, but move it to Microsoft SQL Server later.

This introduction to SQL covers a minute part of its abilities. Many books dedicate their entire subject to SQL. SQL provides the ability to combine tables, filter data, and create powerful procedures. This book covers the major SQL commands necessary to retrieve, update, and modify records in a database.

## SQL Statements

You can use these four statements throughout this chapter to perform the necessary tasks.

The SELECT statement retrieves information from tables. You specify the fields for the command to retrieve followed by a FROM clause. You follow the FROM clause with the name of the table that you want to use. You can use the optional WHERE statement to retrieve only the necessary data using standard comparison operators.

```
Example:
SELECT TotalBalance
FROM Customers
WHERE LastName = 'Smith'
```

The INSERT statement adds a record into a table. After INSERT, specify INTO followed by the name of the table. After the table name, place the field names to set in parentheses. Then use the VALUES clause with the values for the fields in the same order enclosed in parentheses.

```
Example:
INSERT INTO Customers
(LastName, FirstName, TotalBalance)
VALUES ('Smith', 'John', 150.25)
```

## SQL Clauses

You use the WHERE clause to specify records on which the SELECT, UPDATE, and DELETE commands should function. You can use equal, less than, greater than, less than or equal, greater than or equal, or LIKE operators in the clause. When you use LIKE, you specify test string values containing wildcard characters. You can also use AND, OR, and NOT to combine multiple conditions.

```
Example:
WHERE Price < 10.50
WHERE LastName LIKE 'S%'
WHERE FirstName LIKE 'J__n' AND LastName = 'Smith'
```

You use the ORDER BY clause to specify how the SELECT command performs a sort on the data records it returns. After the ORDER BY clause, specify the field on which to sort the records. Place the DESC keyword after the field name to sort in descending order. If you want to sort on one field, then another, separate the sort fields by commas.

```
Example:
SELECT TotalBalance FROM Customers
ORDER BY Price, Quantity DESC
```

```
Example:
SELECT TotalBalance FROM Customers
ORDER BY LastName, FirstName
```

The UPDATE statement changes fields in records that meet a given criteria. Type the table name after the UPDATE statement followed by the SET clause. You then specify field names and new values and use the WHERE clause to identify the records to alter.

```
Example:
UPDATE Customers
SET TotalBalance = 560.50
WHERE LastName = 'Smith'
AND FirstName = 'John'
```

The DELETE statement deletes records from the table that meet given criteria. After the DELETE statement, type FROM followed by the name of the table. Use the WHERE clause to identify the records to delete.

```
Example:
DELETE Customers
WHERE LastName = 'Smith'
AND FirstName = 'John'
```
