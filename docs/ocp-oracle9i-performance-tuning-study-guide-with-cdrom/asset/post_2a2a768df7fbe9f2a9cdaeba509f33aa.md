
Server notes the time (using the System Change Number or SCN) at which Jennifer's query starts in order to show Jennifer the data, as it exists at that moment in time, throughout her query.

- 11:33 A.M.: Malka finishes her phone call and commits her changes to the customer's unpaid balance. This releases the rollback segment entry that previously stored the before-image of her transaction. However, the Oracle Server does note on the Interested Transaction List that Jennifer's process is "interested" in Malka's before-image, since Jennifer's transaction needs the data for read consistency.
- 11:48 A.M.: In order to maintain read consistency, Jennifer's long-running report needs to show the data for the customer that Malka changed, as it existed at 11:32 A.M. Since Malka committed her changes, this data no longer exists in the table, only in the rollback segment. If no other user has happened to use the rollback segment blocks where Malka stored her before-image, Jennifer's Server Process will simply read the blocks and continue. If another user has overwritten the blocks that used to contain Malka's before-image, Jennifer's query will fail with an ORA-01555 SNAPSHOT TOO OLD (rollback segment too small) error because read consistency for Jennifer could not be maintained.

The best protection against the SNAPSHOT TOO OLD error is twofold. First, try to avoid executing long-running queries while short transactions are occurring on the tables underlying those queries. Second, increase the size and number of rollback segments to decrease the likelihood that a released rollback segment entry, i.e. entry that is needed by another session, will be overwritten before they are able to use it.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_485_0.png)

When I create rollback segments on new systems, I use standard sizing values of INITIAL 512K, NEXT 512K, and MINEXTENTS of 20. This formula will result in a 10MB rollback segment. These values tend to prevent most rollback segment problems, but should be monitored nonetheless to determine whether they are too big or too small.

## Explicitly Managing Rollback Segments to Improve Performance

Very large transactions, like those associated with batch processing runs, frequently require large rollback segments, which are not necessarily appropriate for regular OLTP transactions.

**Oracle Objective**

> Appropriately allocate rollback segments to transactions

In these cases, it is best to create one or two large rollback segments and dedicate them to this purpose. However, since the Oracle Server normally assigns transactions to rollback segments automatically, you will need to add a few extra steps to your batch processing in order to utilize this technique:

1. Create a new, large rollback segment for storing the before-images for large batch jobs:

```sql
SQL> CREATE PRIVATE ROLLBACK SEGMENT rbsbatch
  2  STORAGE (INITIAL 10M NEXT 10M)
  3  TABLESPACE rbs;
```

Right after creation, the new rollback segment will be in an offline state. Leave the rollback segment offline until it is time to do the batch processing.

2. Just before starting the batch processing jobs, put the rollback segment online:

```sql
SQL> ALTER ROLLBACK SEGMENT rbsbatch ONLINE;
```

3. Next, assign the batch job to this rollback segment using the `SQL` command `SET TRANSACTION` or the `DBMS_TRANSACTION` stored procedure:

```sql
SQL> SET TRANSACTION USE ROLLBACK SEGMENT rbsbatch;
```
or
```sql
SQL> EXECUTE DBMS_TRANSACTION.USE_ROLLBACK_SEGMENT('rbsbatch');
```

4. Now, start the batch processing job:

```sql
SQL> EXECUTE posting_job;
```

5. Next, from a database session other than the one that is executing the batch job, immediately take the large rollback segment offline:

```sql
SQL> ALTER ROLLBACK SEGMENT rbsbatch OFFLINE;
```

The rollback segment will not actually go offline until the batch transaction is complete. However, because it has been marked to go offline in the data dictionary, no other transactions will be assigned to it. Manually assigning the transaction to its own rollback segment will help ensure that the transaction will find adequate undo space to hold the transaction's before-image.

**WARNING** Any commit that occurs within the batch job will cause the large rollback segment to go offline and become unavailable. Therefore, you must bring the rollback segment back online and reissue the SET TRANSACTION or DBMS_TRANSACTION command after each commit to keep the batch job from using some other rollback segment.

## Minimizing Rollback Segment Activity to Improve Performance

Another way to minimize performance problems related to rollback segments is to try and minimize the number and size of entries that are written to the rollback segments. This goal can be accomplished by performing frequent commits to minimize large rollback entries, using the COMMIT=Y option when performing database imports, forgoing the use of the CONSISTENT option when using the database EXPORT utility, and setting an appropriate COMMIT value when using the SQL\*Loader utility.

**NOTE** See *Oracle9i Database Utilities, Release 1 (9.0.1) (Part Number A90192-01)* for more information on the options for the EXPORT, IMPORT, and SQL\*Loader utilities.

## Using Automatic Undo Management Features to Improve Performance

Oracle9i offers a new feature, Automatic Undo Management (AUM), which relieves the DBA of many of the burdens of manual rollback segment undo (RBU) management described in the previous sections.

Automatic Undo Management (also known as System-managed Undo) is designed to minimize undo segment performance problems by dynamically managing the size and number of undo segments. This concept is similar to the dynamic management of sort segments in temporary tablespaces. With AUM, dedicated tablespaces, called Undo Tablespaces, are created to hold before-image data. The number and size of these undo segments is automatically managed by Oracle based on the demands of the system. The following sections describe techniques for using this new feature to improve undo segment I/O.

**Oracle Objective**

Explain the concept of automatic undo management

### Configuring Automatic Undo Management

In order to utilize AUM in your database, you must first set four init.ora parameters to appropriate values. Descriptions of these parameters are included below.

- **UNDO_MANAGEMENT** Used to indicate whether automatic (AUTO) or manual (MANUAL) undo management is being used in the database. The default is MANUAL.
- **UNDO_TABLESPACE** Specifies the name of the tablespace where the AUM undo segments are to be stored. The default value is the first undo tablespace found during database startup.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_488_0.png)

If no undo tablespace exists, the SYSTEM rollback segment will be used to store undo data.

- **UNDO_RETENTION** Specifies (in seconds) how long to retain undo information after the transaction that generated it commits. The default value is 900 seconds. This parameter is designed to help minimize *Snapshot Too Old* errors caused when a transaction needs overwritten before-image data for read consistency.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_488_1.png)

Undo data can only be retained up to the time specified by *UNDO_RETENTION* when adequate space has been allocated to the undo tablespace.

- **UNDO_SUPPRESS_ERRORS** Used to suppress errors that would otherwise occur when commands that are appropriate in RBU mode (e.g., `SET TRANSACTION USE ROLLBACK SEGMENT ...`) are used in AUM mode.

Once these parameters are configured, you must next create an undo tablespace to hold the system-managed undo segments.

**Oracle Objective**

Create and maintain automatic managed undo tablespace

### Creating an Undo Tablespace

Once the UNDO_MANAGEMENT init.ora parameter has been set to AUTO, you must create a tablespace to hold the system-managed undo segments. The syntax for creating a AUM tablespace is shown here:

```sql
SQL> CREATE UNDO TABLESPACE undo
2  DATAFILE 'd:\oradata\PROD\undo01.dbf' SIZE 500M
3  AUTOEXTEND ON
4  NEXT 5M MAXSIZE 2000M;
```

Once the UNDO tablespace has been created using the above syntax, the parameter UNDO_TABLESPACE=UNDO must be added to init.ora, and the instance restarted before the new tablespace will be used for AUM.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_489_0.png)

You cannot specify the default initial and next extent size for an UNDO tablespace. These values will be system-generated.

The undo tablespace can also be defined at database creation within the CREATE DATABASE statement itself. Figure 8.34 shows an example of this syntax.

**FIGURE 8.34** Undo tablespace specified at database creation

```sql
SQL> CREATE DATABASE PROD
2  MAXDATAFILES 500
3  MAXLOGMEMBERS 4
4  DATAFILE 'D:\oradata\PROD\system01.dbf' SIZE 250M
5  UNDO TABLESPACE rbs DATAFILE 'F:\oradata\PROD\rbs01.dbf' SIZE 500M
6  LOGFILE GROUP 1 ('d:\oradata\PROD\log1a.rdo','e:\oradata\PROD\log1b.rdo') SIZE 5M,
7  GROUP 2 ('d:\oradata\PROD\log2a.rdo','e:\oradata\PROD\log2b.rdo') SIZE 5M;
```
