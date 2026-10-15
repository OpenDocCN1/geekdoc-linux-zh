# Set user information for the DB2 Administration Server

The DB2 Administration Server (DAS) runs on your computer to provide support required by the DB2 tools. A user account with a minimal set of privileges is required to run the DAS. Specify the required user information for the DAS.

+   1. Introduction
+   2. Software Licen...
+   3. Installation type
+   4. Installation acti...
+   5. DAS User
+   6. Instance setup
+   7. Instance use
+   8. Instance-own...
+   9. Fenced user
+   10. Tools catalog
+   11. Contact list
+   12. Contact
+   13. Summary

New user
User name dasusr1
UID
Use default UID
Group name dasadm1
GID 101
Use default GID
Password ******
Confirm password ******
Home directory /home/dasusr1
Existing user
User name
For users of NIS or similar management systems
If the user information in your environment is managed remotely by NIS or a similar system, you must specify an existing user.

![](bbox=[0.78, 0.31, 0.85, 0.48])

Figure 4-1 Create new DAS user

The Set up a DB2 instance window appears (Figure 4-2). If you only want to migrate your existing instances, select the Do not create a DB2 instance option. Select Create a new DB2 instance if you want to create a new instance in addition to the old ones you will be migrating. If you want to create the V8 tools catalog on a separate instance, then we recommend you select Create a new DB2 instance at this point in time. This option allows you to use the DB2 Setup wizard to create the tools catalog on the new instance you are creating.