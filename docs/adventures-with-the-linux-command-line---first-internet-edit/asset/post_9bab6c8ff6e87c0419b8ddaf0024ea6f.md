
keys? Why not, for instance, just use the customer's name as the key? It's because we can't guarantee the name won't change, or that two people might have the same name. We can guarantee that an arbitrarily assigned value like our customer number is unique and immutable.

## Database Engines/Servers

There are a number of database servers available for Linux. The two most prominent MySQL (and its fork MariaDB) and PostgreSQL. These database servers implement client/server architecture, a concept that became a hot topic in the 1990s. Database servers of this type run as server processes and connect to them over a network connection and send SQL statements to the server to carry out. The results of the database operations are returned to the client program for further processing and presentation. Many web sites use this architecture with a web server sending SQL statements to a separate database to dynamically create web pages as needed. The famous LAMP stack consisting of Linux, Apache web server, MySQL, and PHP powered much of the early.

For purposes of this adventure, setting up database servers such as MySQL and PostgreSQL is too complicated to cover here since, among others, they support multiple concurrent users and their attendant security controls. It's more than we need for learning SQL.

## sqlite3

The database we will be using is SQLite. SQLite is a library that can be used with applications to provide a high-level of SQL functionality. It's very popular with the embedded systems crowd. It saves developers the trouble of writing custom solutions to their data storage and management tasks. In addition to the library, SQLite provides a command line tool for directly interacting with SQLite databases. Also, it accepts SQL from standard input (as well as its own command line interface) and sends its results to standard output, it's ideal for use in our shell scripts.

SQLite is available from most Linux repositories. Installation is easy, for:

```
me@linuxbox:-$ sudo apt install sqlite3
```

## Building a Playground

Let's build a playground with some real data. On the LinuxCommand.org site there is an archive we can download that will do trick.

```
me@linuxbox:-$ cd
me@linuxbox:-$ curl -c http://linuxcommand.org/adventure-sql.tgz
me@linuxbox:-$ tar xzf adventure-sql.tgz
me@linuxbox:-$ cd adventure-sql
```

Extracting the .tgz file will produce the playground directory containing the data sets, some demonstration code, and some helpful tools. The data sets we will be working with contain the listings of installed packages on an Ubuntu 18.04 system. This will include the name of packages, a short description of each one, a list of files contained in each package, and their sizes.

```
me@linuxbox:~/adventure-sq$ 
```

All the files are human-readable text, so feel free to give them a look. The data sets in the archive are the .tsv files. These are tab-separated value files. The first one is the package_descriptions.tsv file. This contains two columns of data: a package name and a package description. The second file, named package_files.txt, has three columns: a package name, the name of a file installed by the package and the size of the file.

## Starting sqlite

To launch SQLite, simply use the command sqlite3 followed optionally by a name of file to load our database. If we do not use a file name, SQLite will create a temporary database in memory.

```
me@linuxbox:~/adventure-sq$ sqlite3
SQLite version 3.22.0 2018-01-22 18:45:57
Enter."help" for usage hints.
Connected to a transient in-memory database.
Use ".FILENAME" to reopen on a persistent database.
sqlite>
```

When loading is complete, SQLite will present a prompt where we can enter commands. Commands can be either SQL statements or dot commands that are used to control SQLite itself. To see a list of the available dot commands, we enter .help at the prompt.

```
sqlite> .help
```

There are only a few of the dot commands that be of interest to us and they deal with how output is formatted. To exit sqlite3, we enter the dot command .quit

```
sqlite> .quit
```

Though we can interact directly with the sqlite3 program using the sqlite> prompt, sqlite3 can also accept streams of dot commands and SQL statements through standard input. This is how SQLite is often used. 

## Creating a Table and Inserting Our Data

To get started with our database, we need to convert our .tsv files into a stream of SQL statements. Our database will initially consist of two tables. The first is named Package_Descriptions and the second is named Package_Files. To create the SQL stream for the Package_Descriptions table we will use the insert_Package_Descriptions.awk program supplied in the playground archive.

```
me@linuxbox:~/adventure-sql$ ./Package_Descriptions.awk 
< package_descriptions.tsv > insert_Package_Descriptions.sql
```

Let's take a look at the resulting SQL query. We'll use the head command to display the first lines of the stream.

```
me@linuxbox:~/adventure-sql$ insert_Package_Descriptions.sql
DROP TABLE IF EXISTS Package_Descriptions;
CREATE TABLE Package_Descriptions (
    package_name VARCHAR(60),
    description VARCHAR(120)
);

BEGIN TRANSACTION;
INSERT INTO Package_Descriptions
VALUES ('a2ps', 
'GNU a2ps "Anything to PostScript" converter and pretty-printer\');
INSERT INTO Package_Descriptions
VALUES ('accountservice', 
'query and manipulate user account information');
```

And the last few lines using the tail command.

```
me@linuxbox:~/adventure-sql$ tail insert_Package_Descriptions.sql
VALUES ('zlibamd64', 
'compression library - runtime\');
INSERT INTO Package_Descriptions
VALUES ('zlib186', 
'compression library - runtime\');
INSERT INTO Package_Descriptions
VALUES ('zlib-devamd64', 
'compression library - development\');
INSERT INTO Package_Descriptions
VALUES ('zsh', 
'shell with lots of features\');
INSERT INTO Package_Descriptions
VALUES ('zsh-common', 
'architecture independent files for Zsh');

COMMIT;
```

As we see, SQL is verbose and English-like. English dictates that keywords be in uppercase; however is not required. SQL is case insensitive. White space is not important, but is often used to make the SQL statements easier to read. Statements can span multiple lines but don't have to. Statements are terminated by a semicolon character. The SQL in this adventure is generally formatted in accordance with the style guide written by Simon Holywell in the “Further Reading” section below. Since some SQL can get complicated, visualness when writing code SQL supports two forms of commenting.

- Single line comments are preceded by dashes
- And multi-line comments are done in the style of the programming language /* */

Before we go on, we need to digress for a moment to discuss SQL as standard. While there are ANSI standards, each database server implements SQL differently. Early days weren't any firm standards, partly commercial. Each vendor wanted to make it hard for customers to migrate to competing products so each added unique features to the language to promote the dreaded “vendor lock-in”.

## Creating and Deleting Tables

The first two lines of our SQL stream deletes any existing table named Package_Descriptions and creates a new table with that name. The DROP TABLE statement deletes a table. The optional IF EXISTS clause is used to prevent errors if the table does not exist. There are a lot of optional clauses in SQL. The CREATE TABLE statement defines a new table. As we can see, this will have two columns. The first column, package_name is defined as a variable string up to 60 characters. VARCHAR Here are some of the common data types supported by SQL databases:

| Data Type | Description |
| --- | --- |
| INTEGER | Integer |
| CHAR(n) | Fixed length string |
| VARCHAR(n) | Variable length string |
| NUMERIC | Decimal numbers |
| REAL | Floating point numbers |
| DATETIME | Date and time values |

## Data Types

SQL databases support many types of data. Unfortunately, this varies by vendor. Even in cases where two databases share the same data type name, the actual meaning of the data type can differ. Data types in SQLite are dynamically typed. While other SQL databases, SQLite are not rigidly fixed. Values in SQLite allows many of the common data types found in other databases, it actually supports 4 general types of data storage.

| Data Type | Description |
| --- | --- |
| INTEGER | Signed integers using 1, 2, 3, 4, 6, or 8 as needed |
| REAL | 8-byte IEEE floating point numbers |
| TEXT | Text strings |
| BLOB | Binary large objects (for example JPEG, or MP3 files) |

SQLite data types

In our example above, we specified VARCHAR as the data type for our columns. SQLite is perfectly happy with this, but it actually stores the values in these columns as just TEXT. It ignores the length restrictions in the data type specification. SQLite is extremely
