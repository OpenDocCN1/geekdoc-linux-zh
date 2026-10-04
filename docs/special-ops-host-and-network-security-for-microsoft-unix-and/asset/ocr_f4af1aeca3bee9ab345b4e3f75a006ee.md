# Commenting and SQL Server Implications

Another example our attacks are so successful that they are making good use of the comment operator (--) to negate any other characters that the actual application is appending to the command string. Again, it doesn't mean that database servers not utilizing a comment operator are impervious. Take, for the case where instead of a city, users are asked to enter their age. Since the data is a number, it is likely that the database datatype is also a number and tick marks (') are not required around the requested data. In this case, there is nothing to comment out an attacker can inject if will the developer does not take the time to ensure the user entered a number.

# Defending Against SQL Injection

Defenses against SQL injection should begin and end with the application developer and/or the QA policies and methods therein. Although some third-party software products may claim to help prevent against SQL injection, it is folly to rely on any product to patch and poor coding that occurs in another. The only way to be secure is to patch your code or alert your vendor so they can do. It is understood that code is written by humans and errors will occur, but there are some techniques that you can use to maximize security and keep SQL injection issues at a minimum, which we cover in the next sections.

# Validating All User Input

Take the time to ask yourself a question on each piece of data input by a user: “What if the user is attempting to enter something into the field that was unintended?” Never assume that just because your input screen shows to input a number that the user will do. Validate data types and make sure that numeric data is properly parsed to remove any single quotes that may legitimately exist. For example, if a customer’s address is “1620 Captain’s Walk,” you wouldn’t want your code to throw nasty message over unclosed quotation marks.

```
HTTP 500.100 - Internal Server Error - ASP error
Internet Information Services
Technical Information (for support personnel)
Error Type:
Microsoft: OLE DB Provider for SQL Server (0x80040E14)
Unclosed quotation mark before the character string '',
/secure/default.asp, line 54
```

![](bbox=[0.069, 0.943, 0.287, 0.967])