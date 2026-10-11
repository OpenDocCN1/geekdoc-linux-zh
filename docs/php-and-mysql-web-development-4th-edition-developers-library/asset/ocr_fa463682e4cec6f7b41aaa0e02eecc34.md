# F.9.1  **Standard Options Supported by mysqladmin**

  


`--character-sets-dir` `--host` `--silent`  

`--compress` `--password` `--socket`  

`--debug` `--pipe` `--user`  

`--debug-check` `--port` `--verbose`  

`--debug-info` `--protocol` `--version`  

`--default-character-set` `--set-variable`  

`--help` `--shared-memory-base-name`

`--debug-info` and `--debug-check` are available as of MySQL 5.1.14 and 5.1.21, respectively.

`--silent` causes `mysqladmin` to exit silently if it cannot connect to the server. The `--verbose` option causes `mysqladmin` to print more information for a few commands. `mysqladmin` also supports the standard SSL options.

# F.9.2  **Options Specific to mysqladmin**

+   • `--count=n`, `-c n`  
+   The number of iterations to make when `--sleep` is given. If `--sleep` is given but `--count` is not, `mysqladmin` iterates forever (or until you interrupt it).

+   • `--force`, `-f` (*boolean*)  
+   This option has two effects. First, it causes `mysqladmin` not to ask for confirmation of the `drop db_name` command. Second, even when multiple commands are specified on the command line, `mysqladmin` attempts to execute each command even if errors occur. Normally, `mysqladmin` exits after the first error.

+   • `--no-beep`, `-b` (*boolean*)  
+   Suppresses production of beeps when errors occur. This option was introduced in MySQL 5.1.17.

+   • `--relative`, `-r` (*boolean*)  
+   Shows the difference between the current and previous values when used with `--sleep`. Currently, this option works only with the `extended-status` command.

+   • `--sleep=n`, `-i n`  
+   Executes the commands named on the command line repeatedly with a delay of *n* seconds between each repetition.

+   • `--vertical`, `-E` (*boolean*)  
+   This option is like `--relative`, but displays output vertically.

+   • `--wait[=n]`, `-w[n]`  
+   The number of times to wait and retry if a connection to the server cannot be established. The default value of *n* is 1 if no value is given. If *n* is specified after `-w`, there must be **no intervening space** or the value will not be interpreted correctly.