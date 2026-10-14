
# Table 24-2: (continued)

| Program | Description |
|---|---|
| mysqltest_embedded | Runs canned tests against an embedded MySQL server and compares the results to an expected results file |
| mysqltestmanager | A background program that can manage multiple MySQL server installations |
| mysqltestmanagerc | A command-line client to interface with the mysqltestmanager program |
| mysqltestmanager-pwgen | Generates a password file to use with the mysqltest program |
| mysql_tzinfo_to_sql | Loads the system time-zone tables into MySQL |
| mysql_upgrade | Checks all tables for incompatibilities with the current version of MySQL |
| mysql_upgrade_shell | Utility to run the mysql_upgrade program on non-UNIX systems |
| mysql_waitpid | Sends a KILL signal to the process with the specified pid and waits for it to exit |
| mysql_zap | Sends a KILL signal to any process that matches a specified pattern |

As you can see, quite a few utilities come with the MySQL installation on the Ubuntu server. Most likely you'll never use most of them, but it's good to know they're there (and what they do) in case you need them.

For most normal interactions with the MySQL server you'll use the mysql command-line program, which is discussed in the next section.

## The mysql Command

The mysql command provides an interactive interface to the MySQL server. When you start the command, you'll get an interactive prompt:

```
$ mysql
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 28
Server version: 5.0.67-Debian6.0 (Ubuntu)

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql>
```

From the mysql> prompt you can submit SQL statements and special commands directly to the MySQL server. The mysql command provides a handful of command-line parameters that allow you to customize what it does when you start it. Table 24-3 shows these command-line parameters.

# Table 24-3: The mysql Command Parameters

| Parameter | Description |
|---|---|
| --auto-rehash | Enable database, table, and data field name completion |
| --batch | Display results using the tab character as a field separator, with each row on a separate line |
| --character-sets-dir=path | Define the location where character sets are installed |
| --column-names | Display data field names in results |
| --comments | Preserve comments sent to the server (the default is to suppress comments) |
| --compress | Compress all information sent between the client and the server |
| --database=dbname | Specify the default database to connect to on the server |
| --debug=[options] | Enable debugging, and specify optional debugging settings |
| --debug-info | Display debugging information when mysql exits |
| --default-character-set=name | Define the default character set |
| --delimiter=char | Define the SQL statement delimiter (default is a semicolon) |
| --disable-named-commands | Disable using long-format MySQL commands from the command line |
| --execute=statement | Send the specified SQL statement to the MySQL server and exit |
| --force | Continue if an SQL error occurs |
| --host=hostname | Connect to the specified host |
| --html | Display all output in HTML format |
| --ignore-spaces | Ignore spaces placed after function names |
| --line-numbers | Display line numbers with errors |
| --local-infile[={0|1}] | Enable or disable the local feature of the LOAD DATA INFILE statement |
| --named-commands | Enable long-format MySQL commands |
| --no-beep | Don't produce an audible signal when an error occurs |
| --no-tee | Don't copy output to a file |
| --one-database | Allow SQL statements only for the database specified on the command line |
| --pager=command | Use the specified command to page output (usually the less, more, or cat commands) |
| --password[=passwd] | Specify the user password to connect to the MySQL server (if the password isn't specified, mysql prompts for the password before connecting) |

# Table 24-3: (continued)

| Parameter | Description |
|---|---|
| --port=num | Specify the TCP port of the remote MySQL server (default is 3306) |
| --prompt=str | Specify the command-line prompt to use |
| --protocol=value | Specify how to connect to the MySQL server, either TCP, SOCKET, PIPE, or MEMORY |
| --quick | Don't cache the result from each query |
| --raw | Don't display text boxes around the query results |
| --reconnect | Automatically attempt to reconnect if the connection to the MySQL server is lost |
| --safe-updates | Only allow UPDATE and DELETE statements that use a WHERE clause to specify rows to update or delete (doesn't allow updating or deleting all of the rows at once) |
| --secure-auth | Don't send passwords to servers using the older format |
| --show-warnings | Display any warnings from the server after each SQL statement |
| --sigint-ignore | Ignore attempts to interrupt the program |
| --silent | Display less output, such as the starting version information |
| --skip-column-names | Don't display the data field names in result sets |
| --skip-line-numbers | Don't display line numbers for errors |
| --socket=path | Specify a local socket file to connect to the MySQL server |
| --ssl* | Series of parameters to specify a secure connection to the MySQL server, if supported |
| --table | Display output in table format (the default in interactive mode but not in batch mode) |
| --tee=file | Copy all output to the specified file |
| --unbuffered | Flush the command buffer after each query |
| --user=user_id | Specify a MySQL user account with which to connect to the server |
| --verbose | Display more output than normal |
| --version | Display the version of the mysql program |
| --vertical | Display data field names and values vertically, one data field per line |
| --wait | Retry the connection to the server if it fails |
| --xml | Display all output in XML format |
