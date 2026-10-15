![](bbox=[0.22, 0.09, 0.88, 0.49])

Figure 3-19 Confirmation window

# Command line

Commands to change the settings can be quickly and conveniently entered by using the command line processor: Use

Use GET DATABASE MANAGER CONFIGURATION to show current values.

Use UPDATE DATABASE MANAGER CONFIGURATION USING <parameter> to change current values.

Use RESET DATABASE MANAGER CONFIGURATION to reset all database manager parameters to their default values.

Use AUTOCONFIGURE to let DB2 determine the values using your input about the system, application behavior, and so on.

Example 3-30 Using the command line to change DBm CFG

```
db2 get dbm cfg
db2 update dbm cfg using DFT_MON_BUFPOOL on automatic
db2 get dbm cfg show detail
db2 autoconfigure using mem_precent 60 apply db and dbm
```

# 3.5.2 DB configuration

For allocation and control of system resources, DB2 uses a separate configuration file for every database in a DB2 instance. This file is named SQLDBCON and is stored in /database_path/$DB2INSTANCE/NODE0000/SQL00001/.