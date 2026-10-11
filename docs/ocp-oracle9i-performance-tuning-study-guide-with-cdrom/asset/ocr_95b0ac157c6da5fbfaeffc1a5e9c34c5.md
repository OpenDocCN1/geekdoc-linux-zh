**UNDO_SUPPRESS_ERRORS** Used to suppress errors that would otherwise occur when commands that are appropriate in RBU mode (e.g., `SET TRANSACTION USE ROLLBACK SEGMENT ...`) are used in AUM mode.

Once these parameters are configured, it you must next create an undo tablespace to hold the system-managed undo segments.

# Oracle Objective

# Create and maintain automatic managed undo tablespace

# Creating an Undo Tablespace

Once the UNDO_MANAGEMENT init.ora parameter has been set to AUTO, you must create a tablespace to hold the system-managed undo segments. The syntax for creating a AUM tablespace is shown here:

```
SQL> CREATE UNDO TABLESPACE undo
2  DATAFILE ' d:\oradata\PROD\undo01.dbf' SIZE 500M
3  AUTOEXTEND ON
4  NEXT 5M MAXSIZE 2000M;
```

Once the UNDO tablespace has been created using the above syntax, the parameter UNDO_TABLESPACE=UNDO must be added to init.ora, and the instance restarted before the new tablespace will be used for AUM.

![](bbox=[0.14, 0.59, 0.21, 0.66])

You cannot specify the default initial and next extent size for an UNDO tablespace. These values will be system-generated.

The undo tablespace can also be defined at database creation within the CREATE DATABASE statement itself. Figure 8.34 shows an example of this syntax.

# FIGURE 8.34   Undo tablespace specified at database creation

```
SQL> CREATE DATABASE PROD
2  MAXDATAFILES 500
3  MAXLOGMEMBERS 4
4  DATAFILE 'D:\oradata\PROD\system01.dbf' SIZE 250M
5  UNDO TABLESPACE rbs DATAFILE 'F:\oradata\PROD\rbs01.dbf' SIZE 500M
6  LOGFILE GROUP 1 (\d:\oradata\PROD\log1a.rdo',\e:\oradata\PROD\log1b.rdo') SIZE 5M,
7  GROUP 2 (\d:\oradata\PROD\log2a.rdo',\e:\oradata\PROD\log2b.rdo') SIZE 5M;
```