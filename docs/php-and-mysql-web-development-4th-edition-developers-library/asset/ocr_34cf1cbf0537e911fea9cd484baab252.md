+   QUICK attempts a quick repair of just the indexes; leaves the data file alone.

+   USE_FFM uses the table's .frm file to reinitialize the index file and to determine how to interpret the contents of the data file so that the indexes can be rebuilt. This can be useful if the index has become lost or irrecoverably corrupted. However, it should be treated as a last resort and should be used only if your current version of MySQL is the same as that used to create the table; otherwise, you risk further damage to the table.

If binary logging is enabled, MySQL writes the REPAIR TABLE statement to the binary log unless the LOCAL or NO_WRITE_TO_BINLOG option is given.

REPAIR TABLE produces output in the format described in the entry for CHECK TABLE.

# REPLACE

```
REPLACE [LOW_PRIORITY | DELAYED] [INTO]
    tbl_name [(col_list)]
      (VALUES|VALUE) (expr [, expr] ...) [, (...)] ...

REPLACE [LOW_PRIORITY | DELAYED] [INTO]
    tbl_name [(col_list)]
      {SELECT ... | (SELECT ...)}

REPLACE [LOW_PRIORITY | DELAYED] [INTO]
    tbl_name SET col_name=expr [, col_name=expr] ...
```

The basic action of a REPLACE statement is like that of INSERT, with the exception that if a row to be inserted has a value for a unique index that duplicates the value in a row already present in the table, the old row is deleted before the new one is inserted. For this reason, there is no IGNORE clause option in the syntax of REPLACE. Also, REPLACE has no support for ON DUPLICATE KEY UPDATE. See the description of INSERT for more information.

It's possible for a REPLACE to delete more than one row if the table contains multiple unique indexes. This can happen if a new row matches values in several of the unique indexes, in which case all the matching rows are deleted before the new row is inserted.

REPLACE requires the INSERT and DELETE privileges for the table.

# RESET

```
RESET option [, option] ...
```

The RESET statement is similar to FLUSH in that it affects log or cache information. option values should be chosen from the following list:

+   MASTER deletes the existing binary log files for a replication master server, creates a new file with the numbering sequence set to 000001, and resets the binary log index to name just the new file.