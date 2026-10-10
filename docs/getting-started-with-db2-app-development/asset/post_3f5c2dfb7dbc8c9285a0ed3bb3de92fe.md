
# Chapter 3 – Stored procedures, UDFs, triggers, and data Web services

This chapter focuses on data server-side development using stored procedures, user-defined functions (UDFs) and triggers.

A stored procedure is a database application object that can encapsulate SQL statements and business logic. Keeping part of the application logic in the database provides performance improvements as the amount of network traffic between the application and the database is considerably reduced. In addition, stored procedures provide a centralized location to store your code, so other applications can reuse the same stored procedures.

A UDF allows you to extend the SQL language and encapsulate your business logic.

Triggers are database objects that allow database administrators to have the data server automatically verify the validity of data before insertion, or to audit data after it has been modified.

Data Web services externalize information from a DB2 database by converting SQL scripts or stored procedures into a Web service. This provides a flexible, inexpensive, and convenient solution to companies that need to share information stored in their databases.

In this chapter you will learn about:

- The basics of SQL PL and Java stored procedures
- Developing User-defined functions
- Creating Data Web Services
- Working with IBM Data Studio
- Creating BEFORE, AFTER and INSTEAD OF triggers.

### 3.1 Stored procedures: The big picture

DB2 stored procedures can be written using SQL PL (SQL Procedural Language), C/C++, Java, COBOL, CLR (Common Language Runtime) supported languages, and OLE. In this chapter, we focus on SQL PL procedures because of their popularity, good performance and simplicity. The SQL PL language is based on the SQL/PSM (SQL Persisted Stored Modules) standard. We also discuss briefly how to create a Stored Procedure using the Java language.

> **Note:** New with DB2 9.7 is the support for PL/SQL (Procedural Language / SQL) which is Oracle's data server proprietary procedural language extension to SQL/PSM and is used with stored procedures. The DB2 Express-C edition does not currently support PL/SQL.

*Figure 3.1* illustrates how stored procedures work.

![](img/5f6ba170efa3a607142589708531bef8_85_0.png)

**Figure 3.1 – Network traffic reduction with stored procedures**

At the top left corner of the figure, you see several SQL statements executed one after the other. Each SQL is sent from the client to the data server, and the data server returns the result back to the client. If many SQL statements are executed like this, network traffic increases. On the other hand, at the bottom, you see an alternate method that incurs less network traffic. This second method calls a stored procedure *myproc* stored on the server, which contains the same SQL; and then at the client (on the left side), the CALL statement is used to call the stored procedure. This second method is more efficient, as there is only one call statement that goes through the network, and one result set returned to the client.

Stored procedures can also be helpful for security purposes in your database. For example, you can let users access tables or views only through stored procedures; this helps lock down the server and keep users from accessing information they are not supposed to access. This is possible because users do not require explicit privileges on the tables or views they access through stored procedures; they just need to be granted sufficient privilege to invoke the stored procedures.

> **Note:** For more information about SQL PL stored procedures, watch this video: http://www.channeldb2.com/video/video/show?id=807741:Video:4343

### 3.2 Working with IBM Data Studio

IBM Data Studio 2.2 will be used in this chapter to develop stored procedures, UDFs, and data Web services. IBM Data Studio 2.2 is free. It is not included with DB2, but provided as a separate image; and it comes in two flavors:

- IDE: Allows you to share the same Eclipse (shell sharing) with other products such as InfoSphere Data Architect and Rational products. It also provides support for Data Web services.
- Stand-alone: This version provides almost the same functionality as the IDE version but without support for Data Web services and without shell sharing. The footprint for this version is a lot smaller.

> **Note:** For a thorough coverage about IBM Data Studio, refer to the free eBook *Getting started with IBM Data Studio for DB2* which is part of this DB2 on Campus free book series.

In this chapter we use the IDE version because we demonstrate how to work with Data Web services. The Data Studio images can be downloaded from **www.ibm.com/db2/express**. *Figure 3.2* shows IBM Data Studio 2.2.

![](img/5f6ba170efa3a607142589708531bef8_87_0.png)

**Figure 3.2 – IBM Data Studio 2.2**

In this chapter we focus on the *Data Project Explorer* view highlighted at the top right corner of the figure. This view focuses on data server-side development.

#### 3.2.1 Creating a project

Before you can develop stored procedures, UDFs or Data Web services in Data Studio, you need to create a project. From the Data Studio menu, choose *File -> New -> Project* and choose *Data Development Project*. This is shown in *Figure 3.3*.

![](img/5f6ba170efa3a607142589708531bef8_88_0.png)

**Figure 3.3 – Creating a data development project**

Follow the steps from the wizard to input a name for your project, and indicate which database you want your project associated with. If you do not have any existing database connection, click on the *New* button in the *Select Connection* panel, and a window as shown in *Figure 3.4* will appear.

![](img/5f6ba170efa3a607142589708531bef8_89_0.png)

**Figure 3.4 – New connection parameters**

In Figure 3.4, make sure to choose DB2 for Linux, UNIX and Windows in the Select a database manager field on the left side of the figure. For the JDBC driver drop down menu, the default after choosing DB2 for Linux, UNIX and Windows is the JDBC type 4 driver listed as IBM Data Server Driver for JDBC and SQLJ (JDBC 4.0) Default. Use this default driver and complete the specified fields. For the host field, you can input an IP address or a hostname. In the example IBM Data Studio and the DB2 database reside on the same computer, so localhost was chosen. Ensure to test that your connection to the database is working by clicking on the Test Connection button shown on the lower left corner of the figure. If the connection test was successful, click Finish and the database name will be added to the list of connections you can associate your project to. Select the database, then click Finish and your project should be displayed on the Data Project Explorer view. In this view, if you click on the “+” symbol, you can drill down the project to see different folders such as PL/SQL packages, SQL scripts, stored procedures, etc.

#### 3.2.2 Creating a stored procedure

To create a Java, PL/SQL or SQL PL stored procedure in Data Studio, follow the steps below. Note that stored procedures in other languages cannot be created from Data Studio. In the following steps, we choose SQL (representing SQL PL) as the language for the stored procedure, however similar steps apply to Java and PL/SQL languages.

**Step 1: Write or generate the stored procedure code**

When you want to create a stored procedure, right-click on the Stored Procedures folder and choose New -> Stored Procedure. Complete the information requested in the New Stored Procedure wizard such as the project to associate the procedure with, the name and language of the procedure, and the SQL statements to use in the procedure. By default, Data Studio gives you an example SQL statement. Take all the defaults for all the other panels, or at this point, you can click Finish and a stored procedure is created using some template code and the SQL statement provided before as an example. This is shown in Figure 3.5.

![](img/5f6ba170efa3a607142589708531bef8_90_0.png)

**Figure 3.5 – A sample stored procedure**

In Figure 3.5, the code for the sample stored procedure MYPROCEDURE was generated. You can replace all of this code with your own code. For simplicity, we will continue in this book using the above sample stored procedure as if we had written it.

**Step 2: Deploy a stored procedure**

Once the stored procedure is created, to deploy it, select it from the Data Project Explorer view, right-click on it, and then choose Deploy. Deploying a stored procedure is basically executing the CREATE PROCEDURE statement, compiling the procedure and storing it in the database. Figure 3.6 illustrates this step.
