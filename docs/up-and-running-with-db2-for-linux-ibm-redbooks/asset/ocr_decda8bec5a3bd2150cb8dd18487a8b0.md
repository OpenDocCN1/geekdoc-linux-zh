Then we create the Tools Catalog by CLP as in Example B-2.

# Example: B-2 Creating Tools Catalog by using CLP

```
db2inst1@UDBLNX08:~> db2 "create database toolscat"
DB20000I  The CREATE DATABASE command completed successfully.
db2inst1@UDBLNX08:~> db2 "create tools catalog esecat0 use existing database toolscat"
DB20000I  The CREATE TOOLS CATALOG command completed successfully.
```

In the preceding example, if you want, you can create the new database (here it is TOOLSCAT) via CREATE TOOLS CATALOG with CREATE NEW DATABASE parameter directly; for details regarding the command syntax of CREATE TOOLS CATALOG, refer to IBM DB2 UDB Command Reference V8, SC09-4828.

Then you can check DAS configuration parameters again and you may find that the parameters associated with the Tools Catalog were changed automatically.

# Example: B-3 DAS Tools Catalog parameters changed automatically

```
db2inst1@UDBLNX08:~> db2 get admin cfg

    Admin Server Configuration

Authentication Type DAS                 (AUTHENTICATION) = SERVER_ENCRYPT

DAS Administration Authority Group Name (DASADM_GROUP) = dasadm1

DAS Discovery Mode                      (DISCOVER) = SEARCH
Name of the DB2 Server System           (DB2SYSTEM) = UDBLNX08

Java Development Kit Installation Path DAS (JDK_PATH) = /opt/IBMJava2-131

DAS Code Page                           (DAS_CODEPAGE) = 0
DAS Territory                           (DAS_TERRITORY) = 0

Location of Contact List                (CONTACT_HOST) =
Execute Expired Tasks                   (EXEC_EXP_TASK) = NO
Scheduler Mode                          (SCHED_ENABLE) = ON
SMTP Server                             (SMTP_SERVER) =
Tools Catalog Database                  (TOOLSCAT_DB) = TOOLSCAT
Tools Catalog Database Instance         (TOOLSCAT_INST) = db2inst1
Tools Catalog Database Schema           (TOOLSCAT_SCHEMA) = ESECAT0
Scheduler User ID                       =
```

In addition to the automatic DAS parameters change, within the Tools Catalog Database, a series of new tables are created, with the schema name specified by TOOLSCAT_SCHEMA, here it is ESECAT0. And two new tablespaces with a