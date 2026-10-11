Once statistics have been gathered using the above techniques, they can be copied from one database to another in order to achieve consistency between production and development environments.

# **Oracle Objective**

# **Copy statistics between databases**

# ## Copying Statistics between Databases

One of the common drawbacks of development environments is that they do not accurately reflect the volume of data that will be used in the final production systems. This can lead to unexpectedly poor performance when applications are moved from development to production. To minimize this problem, Oracle9i allows you to copy your optimizer statistics from your production system to a smaller development system. Even though the data volumes on the development system may be smaller, the optimizer behaves the same way it will when presented with the data volume of the production system. This is extremely useful for developers because they can now see the execution plans that will be used in the production environment once the application is migrated.

This statistics migration process is accomplished by exporting the statistics from the production system and then importing them into the development system. The following steps show you how to use the DBMS_STATS package to perform the export and import operations:

+   1. In the production database, create the STATS table in the JOE schema in the TOOLS tablespace. This table will be used to hold the production schema statistics.
+      SQL> EXECUTE DBMS_STATS.CREATE_STAT_TABLE
+      2 ('JOE', 'STATS', 'TOOLS');
+   
+   2. Capture the current statistics for Joe's schema and store them in the newly created STATS table.
+      SQL> EXECUTE DBMS_STATS.EXPORT_SCHEMA_STATS
+      ('JOE', 'STATS');
+   
+   3. Use the Oracle Export utility from the OS command line to export the contents of the STATS table from the production database.
+      $ exp joe/sidney@PROD file=stats.dmp tables=(STATS) log=stats.log