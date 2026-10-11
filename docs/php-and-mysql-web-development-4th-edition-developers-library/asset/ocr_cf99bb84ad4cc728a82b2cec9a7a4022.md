• `--flushlog`
Flushes the logs after all the tables have been locked and before copying them. This has the effect of checkpointing them to the time of the copy operation.

• `--keepold`
If the previous target directory exists, renames it by adding a suffix of _old prior to making a new copy. This option implies --allowold.

• `--method=copy_method`
The method to use for copying files. A value of cp uses the cp program. Experimental support for an scp method is also available. In this case, the `copy_method` value should be the entire scp command to use, and the destination directory must already exist. The scp method may result in your tables being locked for a much longer time than a local copy due to the extra time required to copy the files over the network. To avoid this problem, make the backup locally, and then copy it to the remote host after mysqldump is finished.

• `--noindexes`
Causes index files not to be copied. (If you need to use the backup files later to recover the tables, you can re-create the indexes by using the files with `mysamchk --recover` for MyISAM tables.)

• `--quiet`, `-q`
Causes the program to produce no output except when errors occur.

• `--record-log_pos=db_name.tbl_name`
Before copying tables, causes mysqldump to issue SHOW MASTER STATUS and SHOW SLAVE STATUS statements and record the results in the given table, which should have been created in advance with this structure:

```
CREATE TABLE tbl_name
(
host             VARCHAR(60) NOT NULL,
time_stamp       TIMESTAMP NOT NULL,
log_file         VARCHAR(32) NULL,
log_pos          INT NULL,
master_host      VARCHAR(60) NULL,
master_log_file  VARCHAR(32) NULL,
master_log_pos   INT NULL,
PRIMARY KEY (host)
);
```

The results from SHOW MASTER STATUS are recorded in the `log_file` and `log_pos` columns. This information provides replication coordinates for the binary log; if the backup host is a replication master server, a slave should begin from these coordinates if it is initialized from the backup files as a slave of the master. The results from SHOW SLAVE STATUS are recorded in the `master_host`, `master_log_file`,