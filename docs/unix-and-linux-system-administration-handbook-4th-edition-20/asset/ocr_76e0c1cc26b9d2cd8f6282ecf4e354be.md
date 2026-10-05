# Chapter 20 Electronic Mail

All DB-class tables (dbm, sdbm, hash, and btree) are based on a text file that is compiled to an efficiently searchable binary format. The syntax for these text files is similar to that of the configuration files with respect to comments and continuation lines. Entries are specified as simple key/value pairs separated by white-space, except for aliases, which use a colon after the key to retainmail compatibility. For example, the following lines are appropriate for an alias table:

```
postmaster: david, tobias
webmaster: evi
```

As another example, here's an access table for relaying mail from any client with a hostname ending in cs.colorado.edu

```
.cs.colorado.edu OK
```

Text files are compiled to their binary formats with the postmap command for normal tables and the postalias command for alias tables. The table specification (including the type) must be given as the first argument. For example:

```
$ postmap hash:/etc/postfix/access
$ postmap can query bablabla hash:/etc/postfix/access
$ postmap -q cs.colorado.edu hash:/etc/postfix/access
OK
```

# Local delivery

The local program delivers mail to local recipients. It also handles mail aliasing. For example, if mydestination is set to cs.colorado.edu and email arrives for evi@cs.colorado.edu, local first consults the alias_maps tables and then matches any matching recursively.

If no aliases match, local looks for a forward file in user evi's home directory and follows the instructions in it if it exists. (The syntax is the same as the right side of an alias map.) Finally, if no forward file is found, the email is delivered to evi's local mailbox.

By default, local writes to standard mbox-format files using /var/mail. You can change that behavior with the parameters shown in Table 20.22.

# Table 20.22 Parameters for local mailbox delivery (set in main.cf)

| Parameter | Description |
| mail_spool_directory | Delivers mail to a central directory serving all users |
| home_mailbox | Delivers mail to —user under the specified relative path |
| mailbox_command | Delivers mail with an external program, typically procmail |
| mailbox_transport | Delivers mail through a service as defined in master.cf |
| recipient_delimiter | Allows extended usernames (see description below) |

+   a. This option interfaces with mailbox servers such as the Cyrus imapd.