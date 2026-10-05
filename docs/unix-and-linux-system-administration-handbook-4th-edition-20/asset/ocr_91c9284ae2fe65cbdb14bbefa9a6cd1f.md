# Lookup tables

Another useful option is -n, which makes postconf print only the parameters that differ from the default. If you ask for help on the Postfix mailing list, that's the configuration information you should put in your email.

# Lookup tables

Many aspects of Postfix's behavior are shaped through the use of lookup tables, which can map keys to values or implement simple lists. For example, the default setting for the alias_maps table is

```
alias_maps = dbm:/etc/mail/aliases, nis:mail.aliases
```

Data sources are specified with the notation type:path. Note that this particular table actually uses two distinct sources of information simultaneously: a dbm database and an NIS map. Multiple values can be separated by commas, spaces, or other. Table 20.21 lists the available data sources; postconf -m shows this information.

# Table 20.21 Information sources for Postfix lookup tables

| Type | Description |
|---|---|
| dbm/sdbm | Traditional dbm or group database file |
| cidr | Network addresses in CIDR form |
| hash/btree | Berkeley DB hash or B-tree file (replaces dbm) |
| ldap | LDAP directory service |
| mysql | MySQL database |
| nis | NIS directory service |
| pcre | Perl-Compatible Regular Expressions |
| pgsql | PostgreSQL database |
| proxy | Access through proxymap, e.g., to escape a groot |
| regexp | POSIX regular expressions |
| static | Returns the value specified as path regardless of the key |
| unix | The /etc/passwd and /etc/group files; use NIS syntax* |

+   a. unix:passwd.db is the passwd file, and unix:group is the group.

Use the dbm and sdbm types only for compatibility with the traditional sendmail alias tables. Berkeley DB (hash) is a more modern implementation; it's safer and faster. If compatibility is not a problem, use

```
alias_database = hash:/etc/mail/aliases
alias_maps = hash:/etc/mail/aliases
```

The alias_database specifies the table that is rebuilt by newializes and should correspond to the table that you specify in alias_maps. The reason for having two parameters is alias_maps might include non-DB sources such as mysql or nis that do not need to be rebuilt.

![](bbox=[0.935, 0.235, 0.985, 0.36])