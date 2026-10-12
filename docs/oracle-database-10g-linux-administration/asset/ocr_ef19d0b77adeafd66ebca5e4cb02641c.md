# ## Using an SPFILE

The spfile, or server parameter file, exists on the database server. When starting the Oracle instance, the Oracle database server will start up using the file `$ORACLE_HOME/dbs/initSID.ora`. In an Oracle RAC configuration, the spfile is usually stored on a shared disk, and the `$ORACLE_HOME/dbs/initSID.ora` file consists of one line,

```
`SPFILE='/u03/oradata/test/spfiletest.ora'`
```

This specification simply points the Oracle instance to the shared spfile.

![](bbox=[0.05, 0.3, 0.11, 0.39])

> > **NOTE**
> > All nodes in a RAC cluster can share the same spfile.
> > Since there are instance specific parameters in the spfile, they should be set on a per instance basis.

When using the spfile, it is unnecessary to specify the parameter file in the Oracle startup command. The spfile will automatically be used to start up the Oracle instance. In order to determine what spfile is being used, you can use the Oracle command

```
`SQL> SHOW PARAMETER SPFILE;`
```

This will display the name of the current spfile that is being used. It is recommended that the spfile be used, however, there are some cases where a pfile is convenient.

# ## Creating an SPFILE

The spfile can be created from the Oracle database configuration assistant (DBCA), or it can be created at any time by using the CREATE SPFILE command, as follows:

```
```sql
SQL> CREATE SPFILE='/u03/oradata/test/spfiletest.ora' FROM
PPFILE='/opt/oracle/admin/test/inittest.ora';
```
```

Conversely, you can create a pfile from the spfile by using the CREATE PFILE command, as shown here:

```
```sql
SQL> CREATE PFILE='/opt/oracle/admin/test/inittest.ora' FROM
SPFILE='/u03/oradata/test/spfiletest.ora';
```
```

It is always a good idea to create a pfile from the spfile as a backup. Since the pfile can be modified by a text editor, you can modify it before starting the Oracle instance. The spfile can only be modified from within the Oracle instance and requires Oracle to be running.