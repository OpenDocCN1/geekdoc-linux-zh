character_set_connection and works with the statement in the latter character set. (There is an exception: Any literal string in the statement that is preceded by a character set introducer is interpreted using the character set indicated by the introducer.) collation_connection is used for comparisons between literal strings within statement strings.

+   · character_set_filesystem indicates the filesystem character set. It is used for interpreting literal strings known to refer to filenames in SQL statements such as LOAD DATA. These filename strings are converted from character_set_client to character_set_filesystem before opening the file. The default is binary (no conversion).

Very likely you'll find that most character set and collation variables are set to the same value by default. For example, the following output indicates that client/server communication takes place using the latin1 character set:

```
mysql> SHOW VARIABLES LIKE 'character_set\_%';
```

+-------------------------+--------+
| Variable_name | Value |
+-------------------------+--------+
| character_set_client | latin1 |
| character_set_connection | latin1 |
| character_set_database | latin1 |
| character_set_filesystem | binary |
| character_set_results | latin1 |
| character_set_server | latin1 |
| character_set_system | utf8 |
+-------------------------+--------+

```
mysql> SHOW VARIABLES LIKE 'collation\_%';
```

+--------------------+--------------------+
| Variable_name | Value |
+--------------------+--------------------+
| collation_connection | latin1_swedish_ci |
| collation_database | latin1_swedish_ci |
| collation_server | latin1_swedish_ci |
+--------------------+--------------------+

A client that wants to talk to the server using another character set can change the communication-related variables. For example, if you want to use utf8, change three variables:

```
mysql> SET character_set_client = utf8;
mysql> SET character_set_results = utf8;
mysql> SET character_set_connection = utf8;
```

However, it's more convenient to use a SET NAMES statement for this purpose. The following statement is equivalent to the preceding three SET statements:

```
mysql> SET NAMES 'utf8';
```