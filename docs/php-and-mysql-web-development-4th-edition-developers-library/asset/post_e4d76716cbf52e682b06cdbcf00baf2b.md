
database queries. You'll learn how to write your own programs that access MySQL databases. All of these enhance MySQLs capabilities to handle the requirements of your particular applications.

If you'll be responsible for administrering a MySQL installation, this book will tell you what your duties are and how to carry them out. You'll learn how to create user accounts, perform database backups, set up replication, and make sure your site is secure.

## Road Map to This Book

This book is organized into four parts. The first concentrates on general concepts of database use. The second focuses on writing your own programs that use MySQL. The third is aimed at those readers who have administrative duties. The fourth provides a set of reference appendices.

### Part I: General MySQL Use

- **Chapter 1, "Getting Started with MySQL."** Discusses how MySQL can be useful to you, provides a tutorial that introduces the interactive MySQL client program, covers the basics of SQL, and demonstrates MySQLs general capabilities.
- **Chapter 2, "Using SQL to Manage Data."** Every major RDBMS now available understands SQL, but every database engine implements a slightly different SQL dialect. This chapter discusses SQL with particular emphasis on those features that make MySQL distinctive.
- **Chapter 3, "Data Types."** Discusses the data types that MySQL provides for storing your information, the properties and limitations of each type, when and how to use them, how to choose between similar types, expression evaluation, and type conversion.
- **Chapter 4, "Stored Programs."** Discusses how to write and use SQL programs that are stored on the server side. Types of programs available to you are stored functions and procedures, triggers, and events.
- **Chapter 5, "Query Optimization."** Discusses how to make your queries run more efficiently.

### Part II: Using MySQL Programming Interfaces

- **Chapter 6, "Introduction to MySQL Programming."** Discusses some of the application programming interfaces (APIs) available for MySQL and provides a general comparison of the APIs that the book covers in detail.
- **Chapter 7, "Writing MySQL Programs Using C."** Discusses how to write C programs using the API provided by the MySQL C client library.
- **Chapter 8, “Writing MySQL Programs Using Perl DBI.”** Discusses how to write Perl scripts using the DBI module. Covers standalone command-line scripts and scripts for Web site programming.
- **Chapter 9, “Writing MySQL Programs Using PHP.”** Discusses how to use the PHP scripting language and the PHP Data Objects (PDO) database-access extension to write dynamic Web pages that access MySQL databases.

### Part III: MySQL Administration

- **Chapter 10, “Introduction to MySQL Administration.”** An overview of the database administrator’s duties and what you should know to run a MySQL site successfully.
- **Chapter 11, “The MySQL Data Directory.”** An in-depth look at the organization and contents of the data directory, the area under which MySQL stores databases, logs, and status files.
- **Chapter 12, “General MySQL Administration.”** Discusses how to make sure your operating system starts and stops the MySQL server properly when your system comes up and shuts down. Also includes instructions for setting up MySQL user accounts, and discusses log maintenance, configuring storage engines, tuning the server, and running multiple servers.
- **Chapter 13, “Access Control and Security.”** Discusses what you need to know to make your MySQL installation safe from intrusion, both from other users on the server host and from clients connecting over the network. Explains the structure of the grant tables that control client access to the MySQL server. Describes how to set up your server to support secure connections over SSL.
- **Chapter 14, “Database Maintenance, Backups, and Replication.”** Discusses how to reduce the likelihood of disaster through preventive maintenance, how to back up your databases, how to perform crash recovery if disaster strikes in spite of your preventive measures, and how to set up replication servers.

### Part IV: Appendices

- **Appendix A, “Obtaining and Installing Software.”** Discusses where to get and how to install the major tools and sample database files described in the book.
- **Appendix E,“SQL Syntax Reference.”** Describes each SQL statement supported by MySQL.
- **Appendix F,“MySQL Program Reference.”** Explores the programs provided in the MySQL distribution.

> **Note**
> The following Appendices are located online. Go to www.informit.com/title/9780672329388 to register your book and access these files. Or, please visit www.kitebird.com/mysql-book to access these files.

- **Appendix G,“C API Reference” (online).** Explores the data types and functions in the MySQL C client library.
- **Appendix H,“Perl DBI API Reference” (online).** Discusses the methods and attributes provided by the Perl DBI module.
- **Appendix I,“PHP API Reference” (online).** Discusses the methods provided for MySQL support in PHP by the PDO extension.

## How to Read This Book

Whichever part of the book you happen to be reading at any given time, it’s best to try the examples as you go along. That means you should do two things:

- If MySQL isn’t installed on your system, you should install it or ask someone to do so for you.
- You should get the files needed to set up the sampldb sample database to which we’ll be referring throughout the book.

Appendix A indicates where you can obtain all the necessary components and has instructions for installing them.

If you’re a complete newcomer to MySQL or to SQL, begin with Chapter 1. This provides you with a tutorial introduction that grounds you in basic MySQL and SQL concepts and brings you up to speed for the rest of the book. Then proceed to Chapter 2, Chapter 3, and Chapter 4 to find out how to describe and manipulate your own data so that you can exploit MySQL’s capabilities for your own applications.

If you already know some SQL, you should still read Chapter 2 and Chapter 3. SQL implementations vary, and you’ll want to find out what makes MySQL’s implementation distinctive in comparison to others with which you may be familiar.

If you have experience with MySQL but need more background on the details of performing particular tasks, use the book as a reference, looking up topics on a need-to-know basis. You’ll find the appendices especially useful for reference purposes.

If you’re interested in writing your own programs to access MySQL databases, read the API chapters, beginning with Chapter 6. If you want to produce a Web-based front end to your databases for easier access to them, or, conversely, to provide a database back end for your Web site to enhance your site with dynamic content, check out Chapter 8 and Chapter 9.

If you’re evaluating MySQL to find out how it compares to your current RDBMS, several parts of the book will be useful. Read the SQL syntax and data type chapters in Part I to compare MySQL to the version of SQL that you’re used to, the programming chapters in Part II if you need to write custom applications, and the administration chapters in Part III if you assess the level of administrative support a MySQL installation requires. This information is also useful if you’re not currently using a database but are performing a comparative analysis of MySQL along with other database systems for the purpose of choosing one of them.

## Versions of Software Covered in This Book

The first edition of this book covered MySQL 3.22 and the beginnings of MySQL 3.23. The second edition expanded that range to include MySQL 4.0 and the first release of MySQL 4.1. The third edition covered MySQL 4.1 and the initial releases of MySQL 5.0.

For this fourth edition, the baseline for coverage is MySQL 5.0. That is, the book covers MySQL 5.0 and 5.1, and the early releases of MySQL 5.0. Most of this book still applies if you have a version older than 5.0, but differences specific to older versions usually are not explicitly noted.

The MySQL 5.0 series has reached General Availability status, which means that it is considered stable for use in production environments. There were a lot of changes in earlier pre-production 5.0 releases, and I recommend that you use the most recent version if possible. The current 5.0 version as I write it is 5.0.64. The MySQL 5.1 series is in Release Candidate development (currently at 5.1.25) and should reach General Availability status soon. You’ll need MySQL 5.1 if you want to try features such as the event scheduler or XML support.

If you’re using a version of MySQL older than 5.0, be aware that the following features discussed in this book will not be available to you:

- MySQL 5.0 adds stored functions and procedures, views, triggers, strict input handling, true VARCHAR, and INFORMATION_SCHEMA.
- MySQL 5.1 adds the event scheduler, partitioning, log tables, and XML support.
- For information about older versions, check the MySQL Web site at http://dev.mysql.com/doc/, where you can access the Reference Manual for each version.

I also draw your attention to some topics that are not covered in this book:

- The MySQL Connectors, which provide client access for Java, ODBC, and .NET programs.
