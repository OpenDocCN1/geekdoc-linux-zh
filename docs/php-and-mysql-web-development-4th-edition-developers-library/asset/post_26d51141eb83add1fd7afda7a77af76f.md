
Some variables exist only at the session level. The autocommit variable is one of these. Each client begins with its autocommit mode enabled by default, but can disable it as necessary.

Appendix D, “System, Status, and User Reference,” lists all system variables and indicates which of them can be set at startup time and runtime. The following discussion indicates the syntax for checking system variables and for setting their values.

### 12.6.1.1 Checking System Variable Values

To see the current values of system variables, use `SHOW VARIABLES`:

```sql
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

With a `LIKE` clause, you can restrict output to rows for variables with names that match a given SQL pattern:

```sql
mysql> SHOW VARIABLES LIKE 'key%';
| Variable_name              | Value    |
+----------------------------+----------+
| key_buffer_size            | 8388572  |
| key_cache_age_threshold    | 300      |
| key_cache_block_size       | 1024     |
| key_cache_division_limit   | 100      |
+----------------------------+----------+
```

As of MySQL 5.0.2, a `WHERE` clause can be used to specify general conditions for selecting rows. The following statement finds timeouts that are set to less than 60 seconds:

```sql
mysql> SHOW VARIABLES
    -> WHERE Variable_name LIKE 'timeout%' AND Value < 60;
| Variable_name              | Value    |
+----------------------------+----------+
| connect_timeout            | 10       |
| innodb_lock_wait_timeout   | 50       |
| innodb_rollback_on_timeout | OFF      |
| net_read_timeout           | 30       |
| table_lock_wait_timeout    | 50       |
+----------------------------+----------+
```

`SHOW VARIABLES` returns each variable’s session value if one exists at that level and the global value if not. To specifically request the values of global or session variables, add `GLOBAL` or `SESSION` to the statement:

*   `SHOW GLOBAL VARIABLES;`
*   `SHOW SESSION VARIABLES;`

`LOCAL` is a synonym for `SESSION`.

The `mysqladmin variables` command displays the current values of the server’s global system variables.

Individual variable values can be selected using `@GLOBAL.var_name` syntax for a global variable, or `@SESSION.var_name` or `@LOCAL.var_name` for a session variable. If you use `@var_name` syntax without a level qualifier, the session variable is used if it exists and the global value if not.

The `@`-syntax is general purpose and can be used in `SET`, `SELECT`, or other SQL statements:

```sql
SELECT 'Default storage engine:', @@storage_engine;
```

Most of the session-only variables are not displayed at all by `SHOW VARIABLES`, but you can access their values by name:

```sql
SELECT @@autocommit, @@warning_count;
```

As of MySQL 5.1.12, you can also query the `INFORMATION_SCHEMA` tables named `GLOBAL_VARIABLES` and `SESSION_VARIABLES` to obtain system variable information.

### 12.6.1.2 Setting System Variables at Server Startup Time

Many global system variables can be set when the server starts. There are two syntaxes for doing this:

- You can treat a variable name as an option name and set it directly. For example, the `max_connections` variable controls the maximum number of simultaneous client connections. To set this variable to 200, you can do so using this option on the `mysql` command line:
  - `$ mysql --max_connections=200`

  You can also set the variable in an option file using this syntax:
  
  ```ini
  [mysql]
  max_connections=200
  ```

Another feature of the variable-as-option syntax is that underscores can be given as dashes so that the variable reference looks more like other options. On the command line, set the variable like this:

```bash
$ mysqld --max-connections=200
```

In an option file, set it like this:

```ini
[mysqld]
max-connections=200
```

- You can set a variable at server startup with the `--set-variable` or `-O` option. This syntax is older and is deprecated but still supported for now. On the command line, set a variable like this:

```bash
$ mysqld --set-variable=max_connections=200
$ mysqld -O max_connections=200
```

In option files, only the long-option form is allowable:

```ini
[mysqld]
set-variable=max_connections=200
```

It’s usually more convenient to set system variables in an option file than on the command line because you don’t have to remember to set them each time you start the server. For variables that represent buffer sizes or lengths, values can be in bytes if specified as a number with no suffix, or may be specified with a suffix of ‘K’, ‘M’, or ‘G’, to indicate kilobytes, megabytes, or gigabytes, respectively. Suffixes are not case sensitive, so you can also use ‘k’, ‘m’, or ‘g’.

Some system variables cannot be set directly using a startup option. In such cases, there often is a related option. For example, you cannot directly set the `storage_engine` variable at startup, but the `--default-storage-engine` option can be used instead. Appendix D indicates which global system variables can be set directly. For those that cannot, the appendix lists the related option for setting the variable if there is one.

### 12.6.1.3 Setting System Variables at Runtime

The syntax for setting system variables at runtime depends on whether you want to set a global variable or a session variable. To set a global variable named `var_name`, use a `SET` statement having one of these formats:

```sql
SET GLOBAL var_name = value;
SET @@GLOBAL.var_name = value;
```

To set a session variable, similar syntax applies:

```sql
SET SESSION var_name = value;
SET @@SESSION.var_name = value;
```

`LOCAL` is a synonym for `SESSION`.

If no level indicator is present, the `SET` statement modifies the session variable:

```sql
SET var_name = value;
SET @@var_name = value;
```

You can set several variables in a single `SET` statement by separating the assignments with commas:

```sql
SET SESSION sql_warnings = 0, GLOBAL storage_engine = InnoDB;
```

In a statement that sets multiple variables, an explicit `GLOBAL` or `SESSION` level indicator applies to following variable settings that do not include a level of their own. The following statement sets the global `v1` and `v2` variables, and the session `v3` and `v4` variables:

```sql
SET GLOBAL v1 = val1, v2 = val2, SESSION v3 = val3, v4 = val4;
```

You must have the `SUPER` privilege to set a global variable. The setting persists until changed again or the server exits. No special privileges are needed to set a session variable. The setting persists until changed again or the current connection terminates.

Unlike variables that are set at startup time, you cannot specify runtime values using suffix letters of 'K', 'M', or 'G'. However, you can use expressions, and expressions can refer to the values of other variables. The following statements set the global `read_buffer_size` value to 2MB, and the session value to twice that:

```sql
SET GLOBAL read_buffer_size = 2*1024*1024;
SET SESSION read_buffer_size = 2*@@GLOBAL.read_buffer_size;
```

Many system variables can be set to the special value `DEFAULT`. For those variables that understand this syntax, assigning `DEFAULT` to a global value sets it to the compiled-in default (even if a different value was given with a startup option). Assigning `DEFAULT` to a session variable sets it to the current value of the corresponding global variable.

MySQL supports the concept of a structured system variable, which consists of a set of related system variables that are grouped and accessed as components of the structured variable. Currently, the only structured variables that exist are used for configuring MyISAM key caches, so their syntax is discussed in Section 12.7.2, "Configuring the MyISAM Storage Engine."

## 12.6.2 General-Purpose System Variables

The following list describes several system variables that are useful for general performance tuning:

- `delayed_queue_size` determines the number of rows from `INSERT DELAYED` statements that can be queued per table (for those storage engines that support `DELAYED` inserts) before clients issuing additional `INSERT DELAYED` statements get blocked. If you have many clients that use `INSERT DELAYED` to avoid being blocked but find that they are being blocked anyway because too many rows are being queued, increasing the value of this variable can be useful. That enables a larger queue and
