To check the value of system variables, use the SHOW VARIABLES statement. You can also retrieve individual system variable values by using SELECT:

```
SELECT @@GLOBAL.sql_mode, @@SESSION.sql_mode, @@LOCAL.sql_mode;
```

Section 12.6.1, “Checking and Setting System Variable Values,” further discusses the use of system variables.

The following list describes miscellaneous settings that can be controlled with SET.

+   - SET CHARACTER SET ({charset} | DEFAULT)

Sets the character_set_client and character_set_results session variables to the named character set, and sets the character_set_connection session variable to the value of character_set_database. These variables affect conversion of character data sent to and from the server. A charset value of ucs2, utf8, or utf32 does not work.

SET CHARACTER SET DEFAULT restores the default character set mapping.

+   - SET NAMES ({charset} | '{charset}' | DEFAULT)

Sets the character_set_client, character_set_connection, and character_set_results session variables to the named character set, and sets collation_connection to the default collation for character_set_connection. These variables affect conversion of character data sent to and from the server. A charset value of ucs2, utf8, or utf32 does not work.

SET NAMES DEFAULT restores the default character set mapping.

# SET PASSWORD

```
SET PASSWORD [FOR account] = PASSWORD('pass_val')
SET PASSWORD [FOR account] = OLD_PASSWORD('pass_val')
SET PASSWORD [FOR account] = 'encrypted_pass_val'
```

SET PASSWORD changes the password for a MySQL account. You can always change your own password, unless you have connected as an anonymous user. To change the password for another account, you must have the UPDATE privilege for the mysql database.

With no FOR clause, the statement sets the password for the current account. With a FOR clause, it sets the password for the named account, which should be given in ‘user_name'@'host_name' format, as described in Section 12.4.1.1, “Specifying Account Names.”

The password value, ‘pass_val' should be encrypted using PASSWORD() for standard encryption or OLD_PASSWORD() for the older (pre-MySQL 4.1) encryption. If you use neither function, ‘encrypted_pass_val' should be given as an already-encrypted password string.

```
SET PASSWORD = PASSWORD('secret');
SET PASSWORD FOR 'paul' = PASSWORD('secret');
SET PASSWORD FOR 'paul'@'localhost' = PASSWORD('secret');
SET PASSWORD FOR 'bill'@'%.bigcorp.com' = PASSWORD('old-sneep');
```