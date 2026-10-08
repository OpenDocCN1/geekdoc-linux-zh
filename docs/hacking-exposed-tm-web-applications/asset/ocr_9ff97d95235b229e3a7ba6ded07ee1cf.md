provide a rich library of cryptographic function available to the developer. For sites that are based heavily on script languages, such as ASP, such functions can be encapsulated in COM object.

# Bypassing SQL-Backed Login Forms

On Web sites perform Forms-based authentication with a SQL back-end, SQL injection can be used to bypass authentication (see Chapter 9 for more specific details on the technique of SQL injection). Web site uses databases to store passwords and SQL to query the database to validate authentication credentials. A typical SQL statement will look something like the following (this example has been wrapped across two lines due to page-width constraints):

```
SELECT * from AUTHENTICATIONTABLE WHERE Username = 'username input'
AND Password = 'password input'
```

If input validation is not properly, injecting:

```
Username'
```

in the username field would change the SQL statement to:

```
SELECT * from AUTHENTICATIONTABLE WHERE Username = 'Username' --
AND Password = 'password input'
```

The dashes at the end of the SQL statement specify that the remainder of the SQL statement is comments and should be ignored. The statement is equivalent to:

```
SELECT * from AUTHENTICATIONTABLE WHERE Username = 'Username'
```

And voila! The check for passwords is magically removed!
This is a generic attack that does not require much customization for Forms-based authentication on the Web site, as many of the other attacks for Forms-based authentication. We've seen tools in the underground hacker community that automate this attack.

To take the attack to one higher level, SQL injection can be performed on the password field as well. Assuming the same SQL statement is used, using a password of:

```
DUMMYPASSWORD' OR 1 = 1 --
```

would have a SQL statement of the following (this example has been wrapped across two lines due to page-width constraints):

```
SELECT * from AUTHENTICATIONTABLE WHERE Username = 'Username'
AND Password = 'DUMMYPASSWORD' OR 1 = 1 --
```