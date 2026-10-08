# Hacking Exposed Web Applications

files that they do not expect the user to find or view. These files have names such as xmlserver.js, database.inc, or server.js.

An SQL Server connection string is easy to spot, especially when it has a blank password:

```
strConn = "Provider=SQLOLEDB;Data Source=dotcomdb;Initial Catalog=Demo;
User ID=sa;Passwords=
```

Oracle’s global.js file might have credentials.

# Countermeasures

Each database has its own methods of secure installation and security lockdown. Yet there are steps you can defend against SQL injection attacks at the application level.

# Robust Error Handling

Never pass raw ODBC or other errors to the user. Use generic error pages and error handlers to inform a user of a problem, but not provide system information, variables, or other data. In Java, for example, the best way to accomplish this is through the "try, catch, finally"" method of exception handling.

# Parameter Lists

Place user-supplied data into specific variables. String concatenation is the bane of a secure SQL statement because it provides the easiest way for a user to manipulate the statement with tick marks.

Input validation should be performed on the Web server and items in the database should be strongly typed. A field that uses numeric values should be a type INT, not VARCHAR.

# Stored Procedures

Although not a, user-defined stored procedures are more difficult to break with SQL injection. They require a specific number of parameters in specific places in a specific format. That’s a lot of ሲ to satisfy. Improved performance is often a byproduct of stored procedures—it’s not just for security!

# Running with Least Privilege

The database application should run in a least-privilege situation. Also, the user account that the Web server uses should have limited functionality. Sure, it must read and write to the database, but it doesn’t have to write to the Master database or perform backup duties.