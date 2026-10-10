
- Several Windows services are created.

## B.3.2 Installation on Linux

DB2 installation on Linux is straight-forward and requires the following basic steps:

- Log on as the root user to install DB2.
- After downloading DB2 Express-C for Linux from ibm.com/db2/express, look for the file db2setup, and execute it: `./db2setup`
- Follow the self-explanatory instructions from the wizard. Choosing default values is normally sufficient.
- The following is performed by default during installation:
    - DB2 is installed in `/opt/ibm/db2/V9.7`
    - Three user IDs are created. The default values are listed below:
        - `db2inst1` (instance owner)
        - `db2fenc1` (Fenced user for fenced routines)
        - `dasusr1` (DAS user)
    - Three user groups are created corresponding to the above user IDs:
        - `db2iadm1`
        - `db2fadm1`
        - `dasadm1`
    - Instance `db2inst1` is created
    - The DAS `dasusr1` is created
    - Installation logs are stored in:
        - `/tmp/db2setup.his`
        - `/tmp/db2setup.log`
        - `/tmp/db2setup.err`

## B.4 DB2 Tools

There are several tools that are included with a DB2 data server such as the DB2 Control Center, the DB2 Command Editor, and so on. Starting with DB2 version 9.7, however, most of these tools are deprecated (that is, they are still supported but no longer enhanced) in favor of IBM Data Studio. IBM Data Studio is provided as a separate package not included with DB2. For more information, refer to the eBook *Getting started with IBM Data Studio for DB2*.

### B.4.1 Control Center

Prior to DB2 9.7, the primary DB2 tool for database administration was the Control Center, as illustrated in Figure B.4. This tool is now deprecated, but still included with DB2 servers.

![](img/c4119654311ebf24679359ca130a5ee6_215_0.png)

**Figure B.4 - The DB2 Control Center**

To start the Control Center on Windows use *Start -> Programs -> IBM DB2 -> DB2COPY1 (Default) -> General Administration Tools -> Control Center* or alternatively, type the command `db2cc` from a Windows Command Prompt or Linux shell.

The Control Center is a centralized administration tool that allows you to:

- View your systems, instances, databases and database objects;
- Create, modify and manage databases and database objects;
- Launch other DB2 graphical tools

The pane on the left-hand side provides a visual hierarchy of the database objects on your system(s), providing a folder for Tables, Views, etc. When you double-click a folder (for example, the Tables folder, as shown in Figure B.5), the pane on the top right will list all of the related objects, in this case, all the tables associated with the **SAMPLE** database. If you select a given table in the top right pane, the bottom right pane provides more specific information about that table.

Right-clicking on the different folders or objects in the Object tree will bring up menus applicable to the given folder or object. For example, right-clicking on an instance and choosing *Configure parameters* would allow you to view and update the parameters at the instance level. Similarly, if you right-click on a database and choose *Configure parameters*, you would be able to view and update parameters at the database level.

### B.4.2 Command Line Tools

There are three types of Command Line tools:

- DB2 Command Window (only on Windows)
- DB2 Command Line Processor (DB2 CLP)
- DB2 Command Editor (GUI-based, and deprecated)
- These tools are explained in more detail in the next sections.

#### B.4.2.1 DB2 Command Window

The DB2 Command Window is only available on Windows operating systems; it is often confused with Windows Command Prompt. Though they look the same, the DB2 Command Window, however, initializes the environment for you to work with DB2. To start this tool, use Start -> Programs -> IBM DB2 -> DB2COPY1 (Default) -> Command Line Tools -> Command Window or alternatively, type the command `db2cmd` from a Windows Command Prompt to launch it on another window. Figure B.5 shows the DB2 Command Window.

![](img/c4119654311ebf24679359ca130a5ee6_216_0.png)

**Figure B.5 - The DB2 Command Window**

You can easily identify you are working in the DB2 Command Window by looking at the window title which always includes the words DB2 CLP as highlighted in the figure. From the DB2 Command Window, all commands must be prefixed with `db2`. For example, in the above figure, two statements are issued:

```
db2 connect to sample
db2 select * from staff
```

For Linux, the equivalent of the DB2 Command Window is simply the Linux shell (or terminal) where the DB2 environment has been set up by executing the `db2profile` file. This file is created by default and added to the `.login` file for the DB2 instance owner. By default the DB2 instance owner is `db2inst1`.

#### B.4.2.2 DB2 Command Line Processor

The DB2 Command Line Processor (CLP) is the same as the DB2 Command Window, with one exception that the prompt is `db2=>` rather than an operating system prompt. To start the DB2 Command Line Processor on Windows, use `Start -> Programs -> IBM DB2 -> DB2COPY1 (Default) -> Command Line Tools -> Command Line Processor` or alternatively from a DB2 Command Window or Linux shell type `db2` and press `Enter`. The prompt will change to `db2` as shown in Figure B.6.

![](img/c4119654311ebf24679359ca130a5ee6_217_0.png)

**Figure B.6 - The DB2 Command Line Processor (CLP)**

Note that Figure B.6 also illustrates that when working in the CLP, you do not need to prefix commands with `DB2`. To exit from the CLP, type `quit`.

#### B.4.2.3 DB2 Command Editor

The DB2 Command Editor is the GUI version of the DB2 Command Window or DB2 Command Line Processor as shown in Figure B.7. This tool is deprecated for DB2 version 9.7.

![](img/c4119654311ebf24679359ca130a5ee6_218_0.png)

**Figure B.7 - The DB2 Command Editor**

## B.5 The DB2 environment

Figure B.8 provides a quick overview of the DB2 environment.

![](img/c4119654311ebf24679359ca130a5ee6_219_0.png)

**Figure B.8 - The DB2 Environment**

The figure illustrates a server where DB2 Express-C has been installed. The smaller boxes in light green (Environment Variables, Database Manager Configuration File, Database Configuration File, DB2 Profile Registry) are the different areas where a DB2 server can be configured, and they will be explained in more detail in the next section. The larger dark green box represents an instance which in this example has the name `myinst`.

An instance is an environment where database objects can be created. On the same server, you can create several instances, each of which is treated independently. For example, you can use an instance for development, another one for test, and another one for production. Table B.1 shows some useful commands you can use at the instance level. Note that the commands shown in this section can also be performed from DB2 GUI Tools.

| Command | Description |
|---|---|
| `db2start` | Starts the current instance |
| `db2stop` | Stops the current instance |
| `db2icrt <instance_name>` | Creates a new instance |
| `db2idrop <instance_name>` | Drops an instance |
| `db2ilist` | Lists the instances you have on your system |
| `db2 get instance` | Lists the current active instance |

**Table B.1 - Useful instance-level DB2 commands**

Within an instance you can create many databases. A **database** is a collection of objects such as tables, views, indexes, and so on. For example, in Figure B.8, the database **MYDB1** has been created within instance `myinst`. **Table B.2** shows some commands you can use at the database level.

| Command/SQL statement | Description |
| :--- | :--- |
| `create database <database_name>` | Creates a new database |
| `drop database <database_name>` | Drops a database |
| `connect to <database_name>` | Connects to a database |
| `create table/create view/create index` | SQL statements to create table, views, and indexes respectively |

**Table B.2 - Commands and SQL Statements at the database level**

## B.6 DB2 configuration

DB2 parameters can be configured using the Configuration Advisor GUI tool. The Configuration Advisor can be accessed through the Control Center by right clicking on a database and choosing *Configuration Advisor*. Based on your answers to some questions about your system resources and workload, the configuration advisor will provide a list of DB2 parameters that would operate optimally using the suggested values. If you would like more detail about DB2 configuration, keep reading. Otherwise, use the Configuration Advisor and you are ready to work with DB2!

A DB2 server can be configured at four different levels as shown earlier in Figure B.8:

- **Environment variables** are variables set at the operating system level. The main environment variable to be concerned about is `DB2INSTANCE`. This variable indicates the current instance you are working on, and for which your DB2 commands will apply.
- **Database Manager Configuration File (dbm cfg)** includes parameters that affect the instance and all the databases it contains. *Table B.3* shows some useful commands to manage the dbm cfg.

| Command | Description |
| :--- | :--- |
| `get dbm cfg` | Retrieves information about the dbm cfg |
