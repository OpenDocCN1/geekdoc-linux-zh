directory where InnoDB should write its log files. InnoDB will create only files, not directories, so make sure that the log file directory exists prior to starting the server.

+   innodb_log_file_size, innodb_log_files_in_group

When its logs fill up, InnoDB checkpoints the buffer pool by flushing it to disk. Using larger InnoDB log files reduces the frequency with which the logs fill up, and thus reduces the number of times this flushing occurs. (The tradeoff is that with larger logs, the time for recovery after a crash increases.) You can modify `innodb_log_file_size` to change the size of the log files or `innodb_log_files_in_group` to change the number of files. The important characteristic is the total size of the logs, which is the product of the two values. The total size of the logs must not exceed 4GB.

# ### 12.7.4 Configuring the Falcon Storage Engine

The Falcon storage engine is designed with the goal of being self-tuning and relatively maintenance free so as to simplify administration. For example, Falcon log and tablespace files grow automatically as necessary and free space is reclaimed as it becomes available.

The following list describes some of the Falcon parameters that you might want to change when configuring your server:

+   `falcon_page_size`
+   
+   Falcon writes tablespaces using a fixed page size (4KB by default). You can assign `falcon_page_size` a value in bytes to select a page size. The allowable values are 1KB, 2KB, 4KB, 8KB, 16KB or 32KB. You must configure the page size before Falcon creates any tablespace files. To change the page size if Falcon has already created tablespaces, you must back up and drop your Falcon tables, stop the server and remove the Falcon files, and then restart the server with the new page size and reload the dump file.

+   `falcon_serial_log_dir`
+   
+   The directory in which Falcon creates its log files. The default location is the data directory.

Falcon enables you to create additional tablespaces for table storage. You might do this to distribute storage across multiple physical devices for better I/O efficiency, for example. To create a new tablespace for Falcon tables, use CREATE TABLESPACE:

```
CREATE TABLESPACE myts
ADD DATAFILE '/usr/local/mysql/data/falcon_myts.ftr'
ENGINE = FALCON;
```

By default, Falcon tables are assigned to the default tablespace when they are created. To put a table in your new tablespace, use a TABLESPACE option in the CREATE TABLE statement:

```
CREATE TABLE mytbl (i INT) ENGINE = Falcon TABLESPACE myts;
```