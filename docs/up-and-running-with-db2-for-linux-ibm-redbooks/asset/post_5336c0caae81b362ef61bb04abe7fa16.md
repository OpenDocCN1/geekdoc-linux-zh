
In the remainder of this section, we lead you through a procedure of completing your migration.

- 1. Login as the instance owner.
- 2. Run db2ckmig to verify that a database can be migrated. In the following example, we scanned all cataloged databases and saved results to text file mig.txt.

## Example 4-1 db2ckmig command

```
db2inst1@udblnx02:/opt/IBM/db2/V8.1/instance> ./db2ckmig -e -l /db2home/db2inst1/mig.txt

db2ckmig was successful. Database(s) can be migrated.
```

- 3. Next, we looked at mig.txt to check for any errors and to ensure that the version of DB2CKMIG being run was Version 8, and not a previous version.

## Example 4-2 db2ckmig output

```
db2inst1@udblnx02:/opt/IBM/db2/V8.1/instance> more /db2home/db2inst1/mig.txt

Version of DB2CKMIG being run: VERSION 8.
```

- 4. Now it is safe to migrate the instance. Login as root and run the db2imigr command to migrate your instance to Version 8. Use the following syntax:
  ./db2imigr [-u <fenced_user>] instance_name
  Where, fenced_user represents the fenced user ID, and instance_name represents the name of the instance you are migrating. The fenced user ID is only required if you are migrating from a client instance to a server instance. Our input and output is shown in the following example.

## Example 4-3 Migrating the instance

```
udblnx02:/opt/IBM/db2/V8.1/instance # ./db2imigr db2inst1

db2ckmig was successful. Database(s) can be migrated.
DB110701 Program db2imigr completed successfully.
```

- 5. At this point in time, you may want to check the DB2 level to ensure that your instance is now a Version 8 instance. Our db2level results are shown in Example 4-4. Fortunately, there were no unexpected surprises.

## Example 4-4 Check db2level

```
db2inst1@udblnx02:"/sqllib/db2dump" > db2level
DB21085I Instance "db2inst1" uses "32" bits and DB2 code release "SQL08010" with level identifier "01010106".
```

Informational tokens are "DB2 v8.1.0.8", "s021112", "", and FixPak "1".
Product is installed at "/opt/IBM/db2/V8.1".

6. The next step is to migrate all of your databases to Version 8 format. To do this, login as the instance owner to the machine where the database catalogs are stored, issue db2start, and then run the db2 migrate database command.

Before doing so, check the catalog database partition number to ensure that you are working on the correct partition.

## Example 4-5 Viewing catalog information

```
db2inst1@udblnx02:~> db2 list db directory on /database
Local Database Directory on /database

Number of entries in the directory = 1
Database 1 entry:
Database alias              = ITSODB
Database name               = ITSODB
Database directory          = SQL0001
Database release level      = a.00
Comment                     = ITSO San Jose
Directory entry type        = Home
Catalog database partition number = 0
Database partition number   = 0
```

Next, we started the instance.

## Example 4-6 Starting the instance

```
db2inst1@udblnx02:~> db2start
11-15-2002 16:17:55  1  0  SQL1063N  DB2START processing was successful.
11-15-2002 16:17:55  0  0  SQL1063N  DB2START processing was successful.
SQL1063N  DB2START processing was successful.
```

Now we are ready to migrate the database. To migrate a database, use the following command syntax:

```
db2 migrate database <database_alias> user <user_name> using <password>
```

Where, database_alias represents the database you are migrating, user_name represents the name under which the database is migrated, and password is that user's password. The user and password options are not required if you want to use the current user for the command, as shown in Example 4-7.

## Example 4-7 Migrating the database

```
db2inst1@udblnx02:"/sqllib/db2dump> db2 migrate database itsodb
SQL1103W  The Migrate Database command processing was successful.
```

## 7. Update statistics.

DB2 Version 8 has some statistics that are modified or do not exist in previous versions of DB2. To take advantage of these statistics, you may want to run the runstats command on tables, particularly those tables that are critical to the performance of your SQL queries. The runstats command updates statistics about physical characteristics of a table and associated indexes. The optimizer uses these statistics to find the best access path to data.

## 8. Rebind packages.

Any packages stored in a database are invalidated during migration, but then rebuilt after migration when the V8 database manager uses them for the first time. After migration, run the db2rbind command to rebind these packages.

## 9. Migrate DB2 Explain tables.

The migrate database command does not migrate explain tables. Perform this task if you want to keep explain table information that you previously gathered. If you don’t want to keep this information, you can later recreate the explain tables and gather new information. To migrate explain tables, use the db2exmigr command, as follows:

```
db2exmigr -d <database_name> -e <explain_schema> [-u userid password]
```

Where, database_name is the name of the database where the explain tables are stored, explain_schema represents the schema name of the explain tables to be migrated, and userid and password are the current user’s ID and password. The userid and password parameters are optional.

The db2exmigr command does the following:

- Renames the V6/V7 explain tables.
- Creates a new set of explain tables using EXPLAIN.DDL. This EXPLAIN.DDL is under $INSTHOME/sqllib/misc directory.
- Copies the contents of the old tables to the new tables.
- Drops old explain tables.

## 10. Compare DBM and DB configuration settings, and tablespace and package records from before and after migration to verify that the migration was successful.
