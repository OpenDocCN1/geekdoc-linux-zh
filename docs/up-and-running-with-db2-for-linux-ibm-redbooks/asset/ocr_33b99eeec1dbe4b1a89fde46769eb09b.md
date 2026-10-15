![](bbox=[0.13, 0.09, 0.79, 0.53])

Figure 3-1 Control Center main window

Figure 3-1 shows the Control Center which is started on a Linux system. The Systems tree is expanded to display all databases within the db2inst1 instance.

# 3.2 Preparation for database creation

There are a few configuration tasks that need to be done on Linux and DB2 before creating the database. Here we discuss:

+   - Linux specific configuration
+   - Multi-partition specific configuration

# 3.2.1 Linux-specific configuration

In order to access DB2, each Linux user must set up his or her Linux environment. During creation of an instance, DB2 creates a subdirectory named sqllib in the instance home directory $INSTHOME. In this directory, there are important files such as db2nodes.cfg, db2profile, and userprofile. These files are used to set up the DB2 environment. To set up a user environment to use DB2