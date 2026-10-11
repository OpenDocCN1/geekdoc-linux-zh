
# 1.6 Where to Now?

You know quite a bit about using MySQL now. You can set up a database and create tables. You can put rows into those tables, retrieve them in various ways, change them, or delete them. But the tutorial in this chapter only scratches the surface, and there’s still a lot to know about MySQL. You can see this by considering the current state of our *sampdb* database. We’ve created it and its tables and populated them with some initial data. During the process we’ve seen how to write some of the queries needed for answering questions about the information in the database. But much remains to be done. For example, we have no convenient interactive way to enter new score rows for the grade-keeping project or new member entries for the Historical League directory. We have no convenient way to edit existing rows. And we still can’t generate the printed or online forms of the League directory. These tasks and others are revisited in the upcoming chapters, particularly in Chapter 8, “Writing MySQL Programs Using Perl DBI,” and Chapter 9, “Writing MySQL Programs Using PHP”.

Where you go next in this book depends on what you’re interested in. If you want to see how to finish the job we’ve started with our Historical League and grade-keeping projects, Part II covers how to write MySQL-based programs. If you’re going to serve as the MySQL administrator for your site, Part III of this book deals with administrative tasks. However, I recommend acquiring additional general background in using MySQL first, by reading the remaining chapters in Part I. These chapters provide further information on the syntax and use of SQL statements, discuss how MySQL handles data, and show how to make your queries run faster. A good grounding in these topics will stand you in good stead no matter the context in which you use MySQL—whether you’re running *mysql*, writing your own programs, or acting as a database administrator.

# 2 Using SQL to Manage Data

Structured Query Language (SQL) is the language that the MySQL server understands and is the means by which you tell the server how to perform data management operations. Therefore, fluency with SQL is necessary for effective communication with the server. When you use a program such as the mysql client, it functions primarily as a way for you to send SQL statements to the server to be executed. If you write programs in a language that has a MySQL interface, such as the Perl DBI module or PHP PDO extension, these interfaces enable you to communicate with the server by issuing SQL statements.

Chapter 1, “Getting Started with MySQL,” presents a tutorial introduction to many of MySQL’s capabilities, including some basic use of SQL. Now we’ll build on that material to go into more detail about several areas of SQL implemented by MySQL:

- Changing the SQL mode to affect server behavior
- Naming rules for referring to elements of databases
- Using multiple character sets
- Creating and destroying databases, tables, and indexes
- Obtaining information about databases and their contents
- Retrieving data using joins, subqueries, and unions
- Creating views that provide alternative ways of looking at data in tables
- Using multiple-table deletes and updates
- Performing transactions that enable statements to be grouped or canceled
- Setting up foreign key relationships
- Using the `FULLTEXT` search engine

The items just listed cover a broad range of topics of what you can do with SQL. Other chapters provide additional SQL-related information:

- Chapter 4, “Stored Programs,” discusses how to create and use stored functions and procedures, triggers, and events.
- Chapter 12, “General MySQL Administration,” describes how administrative statements such as GRANT and REVOKE are used for managing user accounts. It also discusses the privilege system that controls what operations accounts are allowed to perform.
- Appendix E, “SQL Syntax Reference,” shows the syntax for SQL statements implemented by MySQL. It also covers the syntax for using comments in your SQL statements.

You can also consult the MySQL Reference Manual, which is especially useful for changes made in the most recent versions of MySQL.

## 2.1. The Server SQL Mode

The MySQL server has a system variable named sql_mode that enables you to configure the SQL mode, which affects several aspects of SQL statement execution. This variable can be set globally and individual clients can change the mode to affect their own connection to the server. This means that any client can change how the server behaves in relation to itself without impact on other clients.

The SQL mode affects behaviors such as handling of invalid values during data entry and identifier quoting. The following list describes a few of the possible mode values:

- `STRICT_ALL_TABLES` and `STRICT_TRANS_TABLES` enable “strict” mode. In strict mode, the server is more restrictive about accepting bad data values. (Specifically, it rejects bad values rather than changing them to the closest legal value.)
- `TRADITIONAL` is another composite mode. It is like strict mode, but enables other modes that impose additional constraints for even stricter data checking. Traditional mode causes the server to behave like more traditional SQL servers with regard to how it handles bad data values.
- `ANSI_QUOTES` tells the server to recognize double quote as an identifier quoting character.
- `PIPES_AS_CONCAT` causes `|` to be treated as the standard SQL string concatenation operator rather than as a synonym for the OR operator.
- `ANSI` is a composite mode. It turns on `ANSI_QUOTES`, `PIPES_AS_CONCAT`, and several other mode values that result in server behavior more like standard SQL than how it operates by default.

Section 3.3, “How MySQL Handles Invalid Data Values,” discusses the SQL mode values that affect handling of erroneous or missing values during data entry. Appendix D, “System, Status, and User Variable Reference,” describes the full set of allowable mode values for the sql_mode variable.

When you set the SQL mode, specify a value consisting of one or more mode values separated by commas, or an empty string to clear the value. Mode values are not case sensitive.
