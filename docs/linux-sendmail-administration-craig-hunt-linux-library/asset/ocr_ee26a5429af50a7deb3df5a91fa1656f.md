# Table 7.1 Valid K Command Type Values (continued)

| Type | Description |
| --- | --- |
| regex | An internal routine that handles regular expressions. |
| sequence | Defines a search list to search multiple databases. |
| switch | References an entry in the nswitch.conf file or the host .conf file to create a database sequence. |
| text | A file database. |

On a Linux system, many of these database types are not used. The internal types are always available, but are set up by Sendmail when they are needed and require no intervention by you, btree and hash are the only two types you are likely to use for the external databases that you create yourself. But even in that case, you will declare the database using a FEATURE macro in the master configuration file; you not create your own K commands in the sendmail.cf file. As noted in Chapter 6, all of the databases created default to hash type.

# The K Command Switches

The switches optionally follow type on the K command line specify optional processing. Table 7.2 lists the switches.

# Table 7.2 Valid K Command Switches

| Switch | Description |
| --- | --- |
| -A | Accepts values from duplicate keys. |
| -a | Appends the specified string to the values returned by the lookup. |
| -f | Preserves uppercase. |
| -k | Identifies the column used as the key in the flat file lookup. |
| -m | Verifies the key but doesn't return a value. |
| -N | Indicates that the keys in the database always end with a null byte. |