> The **AccessFileName** directive can be used in httpd.conf to signify a name other than .htaccess. If this is done, you should make sure to instruct Apache to not serve the corresponding access file.

# **Web Application Vulnerabilities**

It is beyond the scope of this book to mention all possible web application vulnerabilities. However, the attacks that follow offer good examples of the most common vulnerabilities.

# **Exploit Improper Input Validation**

Values can be input to web applications via the submision of HTML forms. Before these values are used by the application, they should be checked for illegal characters. Poorly designed web applications fail to check submitted parameters, causing them to be subject to input validation attacks.

Consider the vulnerability found in PHPNuke, an automated web-based news application. PHPNuke failed to sanitize user-supplied input used to construct SQL queries. This provided a malicious user with the ability to perform unauthorized queries on the database used by the PHPNuke application. More information on this can be found at http://www.securityfocus.com/bid/6887.

The act of exploiting an input validation vulnerability on a web application to perform unauthorized SQL queries is known as SQL injection. Consider the following SQL code executed in a web application:

```
SELECT SSN FROM users WHERE username='$INPUT[id]' ;
```

The id parameter is passed to the application via a HTML form that a user submits. If no input validation is performed, a malicious user may submit the HTML form with the value of id equal to

```
blah' OR 'x'='x
```

which causes the original SQL query to execute the following on the database:

```
SELECT SSN FROM users WHERE username='blah' OR 'x'='x' ;
```

This query will return the SSN values for all accounts in the “users” table! Many poorly designed web applications fail to perform input validation on parameters passed to the system() function call. Most programming languages include the system() function call to execute an external program:

```
system("/bin/echo $i");
```