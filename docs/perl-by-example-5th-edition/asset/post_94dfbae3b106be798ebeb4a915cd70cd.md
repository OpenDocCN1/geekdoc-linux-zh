
Like the English language, with all its dialects, many flavors of SQL evolved. Today's SQL is based on IBM's original implementation, with a considerable number of additions. Standards are created to help specify what should be supported in a language. In 1986, the ANSI designated the SQL standard. It was then revised in 1989, 1992, and 1999. The most commonly used standard today is SQL92, representing the second revision of the original specification (SQL2). Most commercial databases (MySQL, Oracle, Sybase, Microsoft Access, and Microsoft SQL Server) support the full SQL2 and claim to be 100 percent compliant with the standard. However, the standard is quite complex, and, as with different dialects of the English language, various vendors have added extensions to their version of SQL, making it difficult to guarantee that an application will run on all SQL server databases.

In this appendix, we focus on the basic SQL language and examine such concepts as table creation, insertion, deletion, and selection of data.

### B.1.2 Executing SQL Statements

Because the database management system discussed in this book is MySQL, the server being used in the following examples is the MySQL database server, and most of the SQL commands will be executed at the mysql command-line client, although you might prefer to use the MySQL Query Browser. Once connected to the database, you simply type the commands in the mysql console (command-line window; see Figure B.1) as explained in Chapter 15.

![](img/8556abcb353c0991f12099420ec28735_753_0.png)

**Figure B.1** The *mysql* console.

**The MySQL Query Browser.** To run SQL commands in the MySQL Query Browser, type them in the box at the top of the application window and click the Execute button. Once you click the Execute button (the green button to the right of the query window), the result will be displayed in the center of the application as a ResultSet tab (see Figure B.2).

![](img/8556abcb353c0991f12099420ec28735_754_0.png)

### B.1.3 About SQL Commands/Queries

SQL is a computer language, and like languages in general, SQL has its rules, grammar, and a set of special or reserved words. Different variants of the language have evolved over the years because different relational database vendors offer additional features to manipulate data in the name of competition. This section covers the basic SQL commands and syntax. Because SQL has so many commands, they are divided into two major categories: the commands to manipulate data in tables and the commands to manipulate the database itself. There are many excellent tutorials on the Web that cover all the SQL commands and how to use them. See http://www.w3schools.com/sql/default.asp.

**English-like Grammar.** When you create a SQL statement, it makes a request, or "queries" the database, in the form of a statement, similar to the structure of an English imperative sentence, such as "Select your partner", "Show your stuff", or "Describe that bully." The first word in a SQL statement is an English verb, an action word called a command, such as *show*, *use*, *select*, *drop*, and so on. The commands are followed by a list of noun-like words, such as *show databases*, *use database*, or *create databases*. The statement might contain prepositions, such as *in* or *from*. For example:

```
show tables in database
```

or

```sql
select phones from customer_table
```

The language also lets you add conditional clauses to refine your query, such as:

```sql
select companyname from suppliers where supplierid > 20;
```

When listing multiple items in a query, like English, the items are separated by commas; for example, in the following SQL statement, each field in the list being selected is comma-separated:

```sql
select companyname, phone, address from suppliers;
```

If the queries get very long and involved, you might want to type them into your favorite editor, because once you have executed a query, it is lost. By saving the query in an editor, you can cut and paste it back into the MySQL browser or command line without retyping it. Most important, make sure your query makes sense and will not cause havoc on an important database. MySQL provides a *test* database for practice.

### Semicolons Terminate SQL Statements

When searching with Google for "SQL query," one of the top results is a Web site called *thinkgeek.com*, which sells T-shirts and apparel, electronics, gadgets, and home office and computing items. Its ad for the "SQL query" T-shirt reads:

Black tshirt with the following SQL query written in white on front *SELECT * FROM users WHERE clue > 0*. Unfortunately, zero rows are then returned—uh oh. And hey! there is no freakin semi-colon at the end of this query because not everybody under the sun uses the same database with the same console/shell—and there is more than one way to skin a cat. Umkay? Umkay.

The semicolon is the standard way to terminate each query statement. Some database systems do not require the semicolon, but MySQL does (exceptions are the USE and QUIT commands), and if you forget it, you will see a secondary prompt, and execution will go on hold until you add the semicolon, as shown in Figure B.3.

![](img/8556abcb353c0991f12099420ec28735_755_0.png)

```
mysql> show databases
      >
      >;

Database
mysql
northwind
phpmysqladmin
test
4 rows in set (0.0 sec)
```

**Figure B.3** Missing semicolon and the secondary prompt.

**Naming Conventions.** A database and its tables are easier to read when good naming conventions are used.

For example, it makes good sense to make table names plural and field/column names singular. Why? Because a table called *Shippers* normally holds more than one shipper, but the name of the field used to describe each shipper is a single value, such as *Company_Name*, *Phone*, and so on. The first letter in a table or field name is usually capitalized.

Compound names, such as *Company_Name*, are usually separated by the underscore, with the first letter of each word capitalized.

Spaces and dashes are not allowed in any name in the database.

**Reserved Words.** All languages have a list of reserved words that have special meaning to the language. The SQL reserved words are listed in Table B.1. Most of these words will be used in this appendix. (See the MySQL documentation for a complete list of all reserved words.)

| **Table B.1** | SQL Reserved Words |
|---|---|
| ALTER | JOIN |
| AND | LEFT JOIN |
| AS | LIKE |
| CREATE | LIMIT |
| CROSS JOIN | ON |
| DELETE | OR |
| DROP | ORDER BY |
| FROM | RIGHT JOIN |
| FULL JOIN | SELECT |
| GROUP BY | SET |
| INSERT | UPDATE |
| INTO | WHERE |

**Case Sensitivity.** Database and table names are case sensitive if you are using UNIX, but not if you are using Windows. A convention is to always use lowercase names for databases and their tables.

SQL commands are not case sensitive. For example, the following SQL statements are equally valid:

```
show databases;
SHOW DATABASES;
```

Although SQL commands are not case sensitive, by convention, SQL keywords are capitalized for clarity, whereas only the first letter of the field, table, and database names is capitalized.

```
SELECT * FROM Persons WHERE FirstName='John'
```

If performing pattern matching with the `LIKE` and `NOT LIKE` commands, then the pattern being searched for is case sensitive when using MySQL.

### The Result Set

A result set is just another table created to hold the results from a SQL query. Most database software systems even allow you to perform operations on the result set with functions, such as `Move-To-First-Record`, `Get-Record-Content`, `Move-To-Next-Record`, and so on. In Figure B.4, the result set is the table created by asking *mysql* to show all the fields in the table called *shippers*.

```sql
mysql> show fields in shippers;
+-------------+-----------+------+-----+---------+----------------+
| Field       | Type      | Null | Key | Default | Extra          |
+-------------+-----------+------+-----+---------+----------------+
| ShipperID   | int(11)   |      | PRI | NULL    | auto_increment |
| CompanyName | varchar(40)|     |     |         |                |
| Phone       | varchar(24)| YES |     | NULL    |                |
+-------------+-----------+------+-----+---------+----------------+
3 rows in set (0.0 sec)
```

**Figure B.4** The result set is just a table produced from a query.

### B.1.4 SQL and the Database

A database server can support multiple databases. For example, an Oracle or MySQL database server might serve one database for accounting, a second for human resources, a third for an e-commerce application, and so on. To see the available databases, SQL provides the *show* command.

### The show databases Command

To see what databases are available on your database server, use the *show databases* command. The list of databases might be different on your machine, but the *mysql* and *test* databases are provided when you install MySQL. The *mysql* database is required because it describes user access privileges, and the *test* database, as the name suggests, is provided as a practice database for testing how things work.

### FORMAT

```
SHOW DATABASES;
```
