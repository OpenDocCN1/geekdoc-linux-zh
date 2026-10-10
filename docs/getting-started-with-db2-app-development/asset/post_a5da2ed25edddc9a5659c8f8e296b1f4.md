
## Conventions

Many examples of commands, SQL statements, and code are included throughout the book. Specific keywords are written in uppercase bold. For example: A NULL value represents an unknown state. Commands are shown in lowercase bold. For example: The dir command lists all files and subdirectories on Windows®. SQL statements are shown in upper case bold. For example: Use the SELECT statement to retrieve information from a table.

Object names used in our examples are shown in bold italics. For example: The flights table has five columns.

Italics are also used for variable names in the syntax of a command or statement. If the variable name has more than one word, it is joined with an underscore. For example: CREATE TABLE table_name

## What’s next?

We recommend you to review the following books in this book series for more details about related topics:

- Getting started with DB2 Express-C
- Getting started with IBM Data Studio for DB2
- Getting started with Java
- Getting started with C/C++
- Getting started with .NET
- Getting started with Ruby on Rails
- Getting started with PHP
- Getting started with Perl
- Getting started with Python
- Getting started with Open source development
- Getting started with Eclipse

The following figure shows all the different eBooks in the DB2 on Campus book series available for free at ibm.com/db2/books

![](img/5f6ba170efa3a607142589708531bef8_16_0.png)

The DB2 on Campus book series

## About the authors

**Raul F. Chong** is the DB2 on Campus program manager and a DB2 technical evangelist based at the IBM Toronto Laboratory. His main responsibility is to grow the DB2 community around the world. Raul joined IBM in 1997 and has held numerous positions in the company. As a DB2 consultant, Raul helped IBM business partners with migrations from other relational database management systems to DB2, as well as with database performance and application design issues. As a DB2 technical support specialist, Raul helped resolve DB2 problems on the OS/390®, z/OS®, Linux®, UNIX® and Windows® platforms. Raul has taught many DB2 workshops, has published numerous articles, and has contributed to the DB2 Certification exam tutorials. Raul has summarized many of his DB2 experiences through the years in his book *Understanding DB2 - Learning Visually with Examples 2nd Edition (ISBN-10: 0131580183)* for which he is the lead author. He has also co-authored the book *DB2 SQL PL Essential Guide for DB2 UDB on Linux, UNIX, Windows, i/OS, and z/OS (ISBN 0131477005)*, and is the project lead and co-author of many of the books in the DB2 on Campus book series.

**Xiqiang Ji** is a DB2 Advanced Support Engineer in IBM AP DB2 Level 2 support team in Sydney. His main responsibility is to provide technical support for IBM Asia Pacific and worldwide customers for solving various DB2 problems. During the past 5 years, He has helped many DB2 customers across various industries solve many critical technical issues. Before this, He had worked for 5 years as a technical consultant in IBM Software Group supporting IBM Business Partners and Independent Software Vendors in developing DB2 applications and DB2 Business Intelligence solutions.

**Priyanka Joshi** is a software engineer with IBM India software labs working as a DB2 advanced technical support specialist. Her primary responsibility is to provide advanced technical support on DB2 Linux®, UNIX® and Windows (LUW) platforms to IBM worldwide customers. Priyanka joined IBM in 2006 and has since worked for numerous pre-sales and post-sales support engagements for DB2 LUW. She specializes in DB2 - Common Client Technologies and is a certified DB2 professional. Priyanka has been identified as the Knowledge Champion for Asia-Pacific division as part of the Knowledge Centered support initiative in IBM and also is a part of the prestigious Technical Leaders group in IBM, responsible for providing smart solutions to IBM customers in collaboration with other IBM product teams.

**Vineet Mishra** is a software engineer with the DB2 LUW team at the India Software Lab. Vineet Joined IBM in 2007 and specializes in C and C++. His areas of interest are High Availability and Disaster Recovery (HADR), stored procedures & UDFs, Embedded SQL and Operating System Kernel. Vineet is a member of IBM Academic Initiative and IBM University Relationship and actively works towards spreading DB2 (LUW) knowledge in colleges. He frequently responds to queries in the DB2 forum.

**Min Wei Yao** is an application developer focusing on Business Intelligence. Min Wei joined IBM in 2008 and has been working in the IBM Global Business Services area since then. Besides working as a developer, Min Wei also likes to experiment with Linux, and DB2. Min Wei is an IBM certified DB2 application developer and administrator for Linux, UNIX and Windows.

## Contributors

The following people edited, reviewed, provided content, and contributed significantly to this book.

| Contributor | Company / University | Position / Occupation | Contribution |
|---|---|---|---|
| Antonio Cangiano | IBM Toronto Lab | Software Engineer and Technical Evangelist | Partial technical review |
| Praveen Devarao | IBM India Software Lab | Software Engineer, IBM Opensource Technologies for IBM Data Servers | Partial technical review |
| Vinay B. Ganapavarapu | University of New Mexico | Student | Partial technical review |
| Upal Hossain | IBM Toronto Lab | Software Developer, DB2 Information Development Infrastructure | Partial technical review |
| Leon Katsnelson | IBM Toronto Lab | Program Director, IBM Data Servers | Technical review |
| Anil Mahadev | IDUG India | IDUG India chairman, database consultant | Partial technical review |
| Leons Petrazickis | IBM Toronto Lab | Software Developer and Technical Evangelist | Partial technical review |
| Rahul Priyadarshi | IBM India Software Lab | System Software Engineer, IBM open source Technologies for IBM Data Servers | Partial technical review |

## Acknowledgements

We greatly thank the following individuals for their assistance in developing materials referenced in this book:

- Natasha Tolub who designed the cover of this book.
- Susan Visser who assisted with publishing this book.

## Chapter 1 — Introduction to DB2 application development

IBM® DB2® is powerful data server software for managing both relational and XML data. It offers flexibility not only to database administrators, but also to database developers. No matter which language you use to develop your programs, DB2 software ("DB2") provides the drivers, adapters, and extensions you need to work with databases as part of your application. Moreover with DB2 Express-C, you can develop your applications at no cost, with no database size limits, and with the same level of programming language support as the other versions of DB2. Develop once using DB2 Express-C, and you can run on any DB2 edition without any modification required to your application.

In this chapter you will learn about:

- Server-side programming using stored procedures, and user-defined functions
- Client-side programming using different programming languages

### 1.1 DB2 application development: The big picture

DB2 offers database developers the flexibility to take advantage of server-side development features such as stored procedures and user-defined functions, while, application developers can develop client applications using the programming language of their choice. This flexibility is illustrated in Figure 1.1.

![](img/5f6ba170efa3a607142589708531bef8_23_0.png)

**Figure 1.1 - DB2 software is for everyone: Database and application developers**

In *Figure 1.1* the left side represents a client machine where an application programmer develops and runs his program. In this client machine, in addition to the operating system, an IBM Data Server Client may be installed depending on the type of application being developed. An IBM Data Server client includes the required connection drivers such as the JDBC drivers and the ODBC/CLI drivers. These drivers can also be downloaded independently by visiting the IBM DB2 Express-C Web site at http://ibm.com/db2/express .

Using programming tools such as IBM Data Studio, InfoSphere™ Data Architect (IDA), Rational® Software Architect (RSA), Rational Application Developer (RAD), and so on, you can develop your application in your desired programming language. The API libraries supporting these languages are also included with the IBM Data Server Client, so that when you connect to a DB2 Server, all the program instructions are translated appropriately using these APIs into the SQL or XQuery statements understood by DB2. *Table 1.1* provides a short description of the tools mentioned earlier.

| Tool name | Description |
| :--- | :--- |
| IBM Data Studio | IBM Data Studio is a free Eclipse-based tool that allows users to manage their data servers and develop stored procedures, functions and Data Web services. For more details, refer to the ebook *Getting started with IBM Data Studio for DB2*. |
| InfoSphere Data Architect (IDA) | IDA is a modeling tool for your data. It helps you build your database logical design and physical design. For more details, refer to |
