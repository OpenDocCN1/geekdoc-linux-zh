2. Broken Authentication and Session Management 3. Sensitive Data Exposure 4. XML External Entity 5. Broken Access Control 6. Security Misconfiguration 7. Cross-Site Scripting 8. Insecure De-serialization

# 9. Using Components with Known Vulnerabilities

Since OWASP assigns “Injection” the highest priority (I agree. SQLi results in the greatest financial losses to websites overall), let’s discuss it next.

Let’s examine the common type of Injection attack: SQL injection.

**SQL Injection or SQLi SQL or the Structured Query Language is the universal language of relational databases. First developed by IBM in the 1970s (what wasn’t developed by IBM in the 1960s and 1970s?), it is now used in nearly every database management system (DBMS), including MySQL (MariaDB), Microsoft’s SQL Server, IBM’s DB2, Oracle, postgresql, and many others. This language is used primarily to query the database for data, but is also used to delete, update, and insert data.**