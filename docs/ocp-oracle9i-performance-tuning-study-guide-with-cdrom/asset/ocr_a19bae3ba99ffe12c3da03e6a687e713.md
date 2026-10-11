This is only a brief introduction to the STATSPACK utility. For full details see Chapter 21, “Using STATSPACK” in the *Oracle9i Database Performance Guide and Reference Release 1 (9.0.1)* Part Number (A87503-02).

# Configuring STATSPACK

Before using STATSPACK to monitor your database's performance, the PERFSTAT schema that owns all the STATSPACK PL/SQL packages, tables, and indexes must be created. Executing the `SPCREATE.SQL` script while connected to the database as a `SYSDBA` user creates the PERFSTAT schema and all its associated objects.

The default password for the PERFSTAT schema is `PERFSTAT`. For security reasons, this password should be changed immediately after the PERFSTAT user is created.

The `SPCREATE.SQL` script is executed using the following command in SQL\*Plus:

+   • Unix: `$ORACLE_HOME/rdms/admin/sprecreate.sql`

+   • Windows 2000: `$ORACLE_HOME\\rdms\\admin\\spcreate.sql`

During the execution of the `SPCREATE.SQL` script, you will be prompted for the names of the default and temporary tablespaces that should be assigned to the PERFSTAT user. In order to manage the STATSPACK segments more easily, a new 250MB tablespace just for the purpose of holding the PERFSTAT segments should be created. The PERFSTAT segments initially require only about 80MB of tablespace, but will require more over time, as additional performance statistics are stored. The `SPCREATE.SQL` script generates three log files, `SPCUS.R1IS`, `SPECTAB.LIS`, and `SPCPKG.LIS`, which should be examined after execution to confirm that all the STATSPACK components were properly created.

Do not use the `SYSTEM` tablespace as the default or temporary tablespace for the PERFSTAT schema. Doing so will cause the `SPCREATE.SQL` script to fail. If the script does fail during execution, you can run the `SPDROP.SQL` script while logged in as a `SYSDBA` to drop the partially created PERFSTAT schema.