Remember the `slave_user` and `slave_pass` values for later when you tell the slave server how to connect to the master. No other privileges are needed if the account is used only for the single, limited purpose of replication. However, you may want to grant additional privileges to the account if you plan to use it connect to the master from the slave host “manually” with the `mysql` program for testing. Then you won’t be so limited in what you can do. (For example, if REPLICATION SLAVE is the only privilege granted to the account, you might not even be able to see database names on the master server with SHOW DATABASES.)

+   3. Connect to the master server and determine its current replication coordinates by executing SHOW MASTER STATUS:

```
```mysql
mysql> FLUSH TABLES; SHOW MASTER STATUS;

+----------------------------+----------+--------------+------------------+-------------------+
| File                       | Position | Binlog_Do_DB | Binlog_Ignore_DB |                   |
+----------------------------+----------+--------------+------------------+-------------------+
| binlog.000093 |        1707 |              |                  |                   |
+----------------------------+----------+--------------+------------------+-------------------+
```
```

Remember the `File` and `Position` values. You will need them later so that you can tell the slave the point from which to start reading binary log events from the master.

**Important:** You must make sure that no updates occur on the master from the time that you determine its replication coordinates until after you make a snapshot of its data to be transferred to the slave.

+   4. The slave server must begin with an exact copy of the databases to be replicated. Perform the initial synchronization of the slave to the master server by copying the master’s databases to the slave. One way to do this is to make a backup on the master host, and then move it to the slave host and load it into the slave server. Another method is to copy all the databases over the network from the master to the slave. Database backup and copying techniques are discussed elsewhere in this chapter.
+   
+      If you haven’t created any databases or tables on the master, you can skip this step because there is nothing to take a snapshot of.

+   5. Connect to the slave and use CHANGE MASTER TO to configure it with the parameters for connecting to the master server and the initial replication coordinates:

```
```
CHANGE MASTER TO
    MASTER_HOST = 'master_host',
    MASTER_USER = 'slave_user',
    MASTER_PASSWORD = 'slave_pass',
    MASTER_LOG_FILE = 'log_file_name',
    MASTER_LOG_POS = log_file_pos;
```
```