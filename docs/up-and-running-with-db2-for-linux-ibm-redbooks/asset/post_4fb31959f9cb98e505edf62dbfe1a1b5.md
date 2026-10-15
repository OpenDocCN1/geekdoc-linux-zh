
## Post installation tasks

In the previous chapter, we provided a detailed process of installing DB2 Version 8 on Linux. In this chapter we discuss post-installation tasks that should be performed to have a functional DB2 environment. The following topics are covered:

- Control Center setup
Control Center is JAVA-based graphical tool that is used to help you administer your DB2 instances and databases. We explain how to get this tool launched for the first time.
- Preparation for database creation
This section discusses Linux-specific settings for single and multiple database partitions.
- Creating databases
This section provides instructions for creating a database using the database wizard and command line processor.
- DB2 configuration
Here we discuss some important configuration parameters for the instance and database.
- Client access setup
This section discusses installation and configuration of DB2 clients to access DB2 ESE.

### 3.1 Control Center setup

DB2 UDB has a rich set of graphical tools that are used for database administrators to manage the database system and for application developers to develop stored procedures and user defined functions. The Control Center is one of the general administration tools that is used to help you explore and administer your databases. Other such tools include the Command Center, which can be used to generate SQL queries, and the Configuration Assistant, which is an excellent tool for configuring your database environment.

If you want to administer your database server with the Control Center, you must start the DB2 Administrator Server on each host of your database server environment. The DB2 Administrator service setup procedure is provided in Chapter 2, "Installation" on page 23. To start the DB2 Administrator Server, log on to every host as DAS user and issue db2admin start.

If you are logged in as instance owner or privileged DB2 user and have an X-Window started, you can either type in the db2cc & command or use the Start Applications → IBM DB2 menu to start the Control Center. If you started your X-Window as root user, you need to switch to the DB2 instance owner ID and set up the display before you can start the Control Center. The sample commands are displayed below.

# Example 3-1 Start Control Center

```
xhost +
su - db2inst1
export DISPLAY=:0.0
db2cc &
```

The & sign after the command returns the shell prompt, which allows you to use this shell for other commands.

> Note: If you get a JAVA error, verify that you have installed and are using the correct JDK Version, which is Java(TM) 2 Runtime Environment, Standard Edition 1.3.1, and verify that the path setting is correct. The JDK is described in 2.1.6, "Additional software requirements" on page 31.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_94_0.png)

Figure 3-1 Control Center main window

Figure 3-1 shows the Control Center which is started on a Linux system. The Systems tree is expanded to display all databases within the db2inst1 instance.

### 3.2 Preparation for database creation

There are a few configuration tasks that need to be done on Linux and DB2 before creating the database. Here we discuss:

- Linux specific configuration
- Multi-partition specific configuration

### 3.2.1 Linux-specific configuration

In order to access DB2, each Linux user must set up his or her Linux environment. During creation of an instance, DB2 creates a subdirectory named sqllib in the instance home directory $INSTHOME. In this directory, there are important files such as db2nodes.cfg, db2profile, and userprofile. These files are used to set up the DB2 environment. To set up a user environment to use DB2

every time the user logs on to the Linux system, add the following command to the user profile under user's home directory $INSTHOME/.profile:

```
. $INSTHOME/sqllib/db2profile
```

db2profile contains all settings that allow users to work with DB2 databases. Do not modify this file, because db2profile will be replaced after installing a FixPak. If you want to make changes specific to your environment, make changes in $INSTHOME/sqllib/userprofile, which is called by db2profile. This file is useful for setting special environment variables such as TSM parameters.

# Notes:

- $INSTHOME should be replaced with the actual value of the home directory of the instance.
- DB2 provides db2cshrc under $INSTHOME/sqllib for csh users to set up the DB2 environment.

### 3.2.2 Multiple partitioned specific configuration

If you have decided to install DB2 in a multi-partitioned environment, then you must prepare the DB2 instance to run on more than just one node. In a partitioned database system, each database partition server must have the authority to perform remote commands on all of the other database partition servers participating in an instance. To enable this, create an .rhosts file as instance owner in the $INSTHOME directory and change permissions to 600. To create the .rhosts file, enter the following command:

```
vi /db2home/db2inst1/.rhosts
```

The format of .rhosts is as follows:

```
hostname instance_owner or user_name
```

Where, hostname is either the hostname or IP address of the physical machine. In Example 3-2, the user db2inst1 has permission to perform remote commands on the hosts udblnx02 and udblnx05.

# Example 3-2 .rhosts file

```
udblnx02 db2inst1
udblnx05 db2inst1
```

To change the .rhosts file permissions to 600, enter the following command:

```
chmod 600 /db2home/db2inst1/.rhosts
```
