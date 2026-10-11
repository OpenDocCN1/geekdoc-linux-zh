Some variables exist only at the session level. The autocommit variable is one of these. Each client begins with its autocommit mode enabled by default, but can disable it as necessary.

Appendix D, “System, Status, and User Reference Reference,” lists all system variables and indicates which of them can be set at startup time and runtime. The following discussion indicates the syntax for checking system variables and for setting their values.

# 12.6.1.1 Checking System Variable Values

To see the current values of system variables, use SHOW VARIABLES:

```
mysql> SHOW VARIABLES;
| Variable_name            | Value    |
+-------------------------+----------+
| auto_increment_increment | 1        |
| auto_increment_offset    | 1        |
| autocommit               | ON       |
| automatic_sp_privileges  | ON       |
| back_log                 | 50       |
| basedir                  | /usr/local/mysql |
| big_tables               | OFF      |
| ...
```

With a LIKE clause, you can restrict output to rows for variables with names that match a given SQL pattern:

```
mysql> SHOW VARIABLES LIKE 'key%';
| Variable_name              | Value    |
+----------------------------+----------+
| key_buffer_size            | 8388572  |
| key_cache_age_threshold    | 300      |
| key_cache_block_size       | 1024     |
| key_cache_division_limit   | 100      |
+----------------------------+----------+
```

As of MySQL 5.0.2, a WHERE clause can be used to specify general conditions for selecting rows. The following statement finds timeouts that are set to less than 60 seconds:

```
mysql> SHOW VARIABLES
    -> WHERE Variable_name LIKE 'timeout%' AND Value < 60;
| Variable_name              | Value    |
+----------------------------+----------+
| connect_timeout            | 10       |
| innodb_lock_wait_timeout   | 50       |
| innodb_rollback_on_timeout | OFF      |
```