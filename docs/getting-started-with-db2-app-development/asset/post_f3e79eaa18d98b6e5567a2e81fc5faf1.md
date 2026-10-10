
Listing 6.9 - C# ADO.NET code snippet (ODBC .NET Data Provider)

There is an extra step needed in Step 1, previously described, when using the ODBC .NET Data Provider:

**Step 1: Configuring connectivity**

- The DB2 database must be cataloged as an ODBC data source. To catalog an ODBC data source follow the steps given below:
    - `db2 catalog system ODBC data source <database name>`
      or
    - `db2 catalog user ODBC data source <database name>`

- To list ODBC data sources:
    - `db2 list system ODBC data sources`
      or
    - `db2 list user ODBC data sources`

Compiling and executing steps are the same as listed before.

## 6.5 Data Manipulation using .NET

The following C# sample code snippets illustrate the methods to SELECT, INSERT, UPDATE and DELETE using the IBM Data Server Provider for .NET classes -- DB2Connection, DB2Command, and DB2Transaction.

Listing 6.10 illustrates how to perform a SELECT.

```csharp
(1) cmd.CommandText = "SELECT deptnum, location " + " FROM org " + " WHERE deptnum < 25";
(2) DB2DataReader reader = cmd.ExecuteReader();
```

Listing 6.10 - C# code demonstrating a SELECT

Let's review each of the items shown in Listing 6.10:

- (1) The `cmd.CommandText` specifies the query to be executed using the connection established before.
- (2) The reader is an instance of the DataReader object and executes the command using the `cmd.ExecuteReader` method. The ExecuteReader method sends the CommandText to the Connection and builds a DB2DataReader.

Listing 6.11 illustrates how to perform an INSERT.

```csharp
// Use the INSERT statement to insert data into the 'staff' table.
cmd.CommandText = "INSERT INTO staff(id, name, dept, job, salary) " +
" VALUES(380, 'Pearce', 38, 'Clerk', 13217.50)," +
" (390, 'Hachey', 38, 'Mgr', 21270.00), " +
" (400, 'Wagland', 38, 'Clerk', 14575.00)";
cmd.ExecuteNonQuery();
```

Listing 6.11 - C# code demonstrating an INSERT

Let's review the item shown in Listing 6.11:

- (1) The `cmd.ExecuteNonQuery` executes an SQL statement against the connection and returns the number of rows affected.

Listing 6.12 illustrates how to perform an UPDATE.

```csharp
// This method demonstrates how to update rows in a table
cmd.CommandText = "UPDATE staff " +
" SET salary = (SELECT MIN(salary) " +
" FROM staff " +
" WHERE id >= 310) " +
" WHERE id = 310";
cmd.ExecuteNonQuery();
```

Listing 6.12 - C# code demonstrating an UPDATE

Listing 6.13 illustrates how to perform DELETEs.

```csharp
// This method demonstrates how to delete rows from a table
{
try
cmd.CommandText = "DELETE FROM staff " +
" WHERE id >= 310 " +
" AND salary > 20000";
cmd.ExecuteNonQuery();
```

Listing 6.13 - C# code demonstrating a DELETE

### 6.5.1 Building and Running the sample program

The code snippets shown above were taken from the program `TbUse.cs` which is part of the sample programs provided with DB2 and can be found under the directory `C:\Program Files\IBM\SQLlib\samples\.NET\cs`.

To run the program follow these steps:

1. Compile the `TbUse.cs` file with `bldapp.bat` from a DB2 Command Window as follows:
    - `bldapp TbUse`
    - or compile `TbUse.cs` with the makefile by entering the following at the command prompt:
    - `rmake TbUse`

2. Run the `TbUse` program by entering the program name at the command prompt:
    - `TbUse`

> **Note:** For more information about sample programs, refer to:
> [http://public.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.samp.top.doc/doc/c0007609.html](http://public.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.samp.top.doc/doc/c0007609.html)

## 6.6 Exercises

Write a small C# program to access BLOB data in the `SAMPLE` database. Follow these steps:

1. Run the following command from a DB2 Command Window to create the `SAMPLE` database if it was not already created: `db2samp1`
2. Write a C# program to update and retrieve BLOB and CLOB data from the `EMP_PHOTO` and `EMP_RESUME` tables. If you find this exercise difficult to do, the sample program for this exercise is provided in the project `db2lobs.zip`, under the “Retrieving and updating BLOBs and CLOBs” section in the following link: [http://www.ibm.com/developerworks/data/library/techarticle/0304surange/0304surange.html#resources](http://www.ibm.com/developerworks/data/library/techarticle/0304surange/0304surange.html#resources)
3. Modify the schema name in the program appropriately and test it.
4. To Run the C# program, follow the steps listed in section 6.5.1.

## 6.7 Summary

In this chapter, you have learned how to set up the environment to develop .NET applications using DB2. You learned the various types of data providers and the way you need to code depending on the provider chosen. The IBM Data Server data provider for .NET is the recommended one because it is best for performance. You also learned about the IBM Database Add-Ins for Visual Studio. The chapter also discussed how to connect to a DB2 database, and how to manipulate DB2 data using sample programs.

## 6.8 Review questions

1. What is the difference between the FieldCount and HasRows public properties of the DataReader object?

2. What configuration do you need to do differently when using the ODBC .NET Data Provider?

3. Name and explain the two components on which the Data Access in ADO.NET relies on.

4. Can you use a 32-bit IBM Data Server Provider for .NET on a 64-bit computer?

5. How can you use the Visual Studio Add-Ins with DB2?

6. The key component of disconnected data access in ADO.NET is:
    - A. DataSet
    - B. DataReader
    - C. Connection
    - D. DataAdapter
    - E. None of the above

7. Which of the following component classes populates a disconnected DataSet with data?
    - A. Command object
    - B. DataReader object
    - C. DataAdapter object
    - D. Dataset
    - E. None of the above

8. Which public property of the Command object is used to describe whether an SQL statement or a stored procedure will be executed?
    - A. CommandText
    - B. CreateParameter
    - C. ExecuteNonQuery
    - D. CommandType
    - E. None of the above

9. All data providers listed below are the .NET data providers for DB2 applications to access a database EXCEPT?
    - A. IBM Data Server Provider for .NET
    - B. Microsoft .NET Data Server Provider
    - C. OLE DB .NET Data Provider
    - D. ODBC .NET Data Provider
    - E. None of the above

10. In IBM Database Add-Ins for Visual Studio, what is used to create and manage DB2 Projects?
    - A. Object Browser
    - B. Server Explorer
    - C. Solution Explorer
    - D. Device Emulator Manager
    - E. None of the above

# 7

## Chapter 7 - Application development with Ruby on Rails

Ruby is an open source, free, dynamic programming language. Ruby on Rails (RoR), or Rails for short is a framework built using Ruby. RoR is based on the Model, View and Controller (MVC) architecture. By supporting agile development techniques it has enabled many developers to radically reduce the time and pain involved in creating Web applications.

In this chapter you will learn about:

- Ruby on Rails and the MVC architecture
- How to setup Ruby on Rails to work with DB2
- A basic understanding of ways to program RoR applications with DB2
- How to build a simple Ruby on Rails application with DB2

### 7.1 Ruby on Rails applications with DB2: The big picture

Ruby on Rails is organized around the Model, View, and Controller architecture, usually just called MVC. MVC benefits include:

- Isolation of business logic from the user interface
- Making it clear where different types of code belong for easier maintenance

A Model represents the information (data) of the application and the rules to manipulate that data. In the case of Rails, models are primarily used for managing the rules of interaction with a corresponding database table. In most cases, one table in your database will correspond to one model in your application. The bulk of your application’s business logic will be concentrated in the model. Under this architecture, DB2 provides data persistence.

Controllers provide the “glue” between models and views. In Rails, controllers are responsible for processing the incoming requests from the Web browser, interrogating the models for data, and passing that data on to the views for presentation.
