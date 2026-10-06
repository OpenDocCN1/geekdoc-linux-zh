# UNIX SYSTEM MANAGEMENT PRIMER PLUS

Next, attempt to query the database servers. You might be tempted to ping the database server to verify access and move on to the next step, but ping doesn't determine whether or not the database server queries you. You don't need simply to access the database server you need to query the database that resides on it. Query verification tools vary among database servers, if, for example, your system uses an Oracle 8i server, you can test the query using Oracle's tnping utility to verify that you can talk to the database (and, by association, the machine), as follows:

```
web$ tnping accounts
tns Ping Query for Solaris: Version 8.1.7.0.0 - Production on 21-DEC-2001
21:59:14
```

> (Copyright) 1997 Oracle Corporation. All rights reserved.
Attempting to contact (ADDRESS=(PROTOCOL=TCP) (HOST=accountdb) (PORT=1521))
OK (0 msec)

In this example, the database query works. You may complete the test by running an actual SQL*Plus command-line utility. This example tests to see if you can view all account balances over $10,000:

```
bash$ sqlplus web@accounts
SQL*Plus: Release 8.1.7.0.0 - Production on Fri Dec 21 22:03:56 2001
(c) Copyright 2000 Oracle Corporation. All rights reserved.
Enterter password:
Connected to:
Oracle8 Release 8.1.7.1.0 - Production
JServer Release 8.1.7.1.0 - Production
SQL> select balance from savings where balance > 10000;
BALANCE
-------

145,000.32
53,231.10
11,242.41
```

# Create Dummy Data for Testing

Newly created databases (and other data stores) are not likely to contain useful data for your test. Consider creating a dummy database with data that can be used for testing but is discarded afterwards.

The account clearly worked, so you are ready to test the functionality of the Apache Web server. Using an analog phone line at the office, dial out to an ISP to access the New Web's site page. Because most users will access the site from outside the network, using an outside provider to test the Web server gives more useful results than testing it from your own network. If the site is accessible, Click on links, attempt to access bank account data, and test links to external sites. If the site is accessible, you can navigate through the site's hyperlinks without failure, and you test is successful and you can move on to the next test.

![](bbox=[0.153, 0.623, 0.213, 0.663])