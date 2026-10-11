```
+-------------------------+
| abcd        | ABCD      |
+-------------------------+
```

Why doesn't UPPER() convert the binary string to uppercase? This happens because the string has no character set, so there is no way to know which byte values correspond to uppercase or lowercase characters. To use a binary string with functions such as UPPER() and LOWER(), you must first convert it to a non-binary string:

```
mysql> SELECT @s1, UPPER(CONVERT(@s1 USING latin1));
```

```
+--------------------------+--------------------------+
| @s1  | UPPER(CONVERT(@s1 USING latin1)) |
+--------------------------+--------------------------+
| abcd | ABCD    |
+--------------------------+--------------------------+
```

# 3.1.2.2 Character Set-Related System Variables

The server maintains several system variables that are involved in various aspects of character set support. Most of these variables refer to character sets and the rest refer to collations. Each of the collation variables is linked to a corresponding character set variable.

Some of the character set variables indicate properties of the server or the current database:

+   character_set_system indicates the character set used for storing identifiers. This is always utf8.

+   character_set_server and collation_server indicate the server’s default character set and collation.

+   character_set_database and collation_database indicate the character set and collation of the default database. These are read-only and set automatically by the server whenever you select a default database. If there is no default database, they’re set to the server’s default character set and collation. These variables come into play when you create a table but specify no explicit character set or collation. In this case, the table defaults are taken from the database defaults.

Other character set variables influence how communication occurs between the client and the server:

+   character_set_client indicates the character set in which the client sends SQL statements to the server.

+   character_set_results indicates the character set in which the server returns results to the client. “Results” include data values and also metadata such as column names.

+   character_set_connection is used by the server. When it receives a statement string from the client, it converts the string from character_set_client to