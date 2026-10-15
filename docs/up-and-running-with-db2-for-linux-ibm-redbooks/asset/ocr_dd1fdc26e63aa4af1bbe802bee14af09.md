To increase space in a DMS tablespace, you can add additional containers.

+   Ensure that you have sufficient log file space prior to migration. We recommend that you significantly increase the values of logfilsiz, logprimary, and logsecond to prevent log file space from running out. The amount of required space depends on your system setup.

For instance, if you want to change the size of logfilsiz from 1000 to 2000, connect to the database and enter the following command:

```
db2 update db cfg using logfilsiz 2000
```

# Migration test consideration

The entire migration process consists of two parts: (1) Installing DB2 Version 8 code, and (2) Migrating instances and databases. Installing DB2 Version 8 does not require system down time. Migrating instances and databases is the actual step which converts your DB2 system from Version 6 or 7 to Version 8. You need to stop DB2 to perform the instances and databases migration.

We recommend that you install and test Version 8 before migrating any Version 6 or Version 7 instances to Version 8. If you have a test environment which is a mimic of the production system, you can install DB2 V8, migrate DB2 instances and databases, test your applications on the test system, and then carry the same procedure to the production environment. However, if you have limited test environment or no test environment, you can utilize the DB2 features to test your applications under the new version.

Since multiple versions of DB2 can coexist on Linux, you can install DB2 Version 8 while the application is still up and running under Version 6 or 7. You can then create Version 8 test instances and databases to test your applications while production transactions are running.

When you are convinced to move your production systems up to Version 8, after making any required changes in your applications or environment, you can do the instances and databases migration during off-peak times to reduce system down time and reduce the number of people or systems affected by that downtime.

If you want to skip testing Version 8 and go directly to migration, you still can consider installing Version 8, while your existing instance(s) continue to run, again to reduce system down time.