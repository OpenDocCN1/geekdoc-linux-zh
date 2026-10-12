# # Upgrading the Linux Operating System

Upgrading the Linux Operating System is something that should be done with great care. I do not recommend using *up2date* (Red Hat) or YAST (SUSE) to automatically update the system because of the potential for problems. The Oracle system has a certain set of requirements that you have seen in previous chapters. The Oracle system depends on specific versions of *gcc*, *libstdc*, *openmotif*, *make*, *binutils*, and the Java Runtime Environment. When you automatically update your system, many of these components could be updated as well. This might or might not cause issues with the Oracle system. So, if you update your system automatically, you are doing this at your own risk.

Let's look at some of the Oracle tasks that you are expected to do as an Oracle DBA.

# # Starting Up the Instance

One of the most basic database administrative tasks is starting up and shutting down the instance. That in itself sounds simple enough, but there are multiple ways to fully start or open an Oracle database, depending on the situation. If we want to start up and open the database, then all that needs to be done is simply to authenticate to the database via *sqlplus* with a user with *sysdba* or *sysoper* system privileges, and issue the startup command.

```
```
sqlplus
SQL*Plus: Release 10.1.0.2.0 - Production on Mon Jun 21 18:55:06 2004

Copyright (c) 1982, 2004, Oracle. All rights reserved.

Enter user-name: sys as sysdba
Enter password:
Connected to an idle instance.

SQL> startup
ORACLE instance started.

Total System Global Area 188743680 bytes
Fixed Size 778036 bytes
Variable Size 162537676 bytes
Database Buffers 25165824 bytes
Redo Buffers 262144 bytes
Database mounted.
Database opened.

SQL>
```
```