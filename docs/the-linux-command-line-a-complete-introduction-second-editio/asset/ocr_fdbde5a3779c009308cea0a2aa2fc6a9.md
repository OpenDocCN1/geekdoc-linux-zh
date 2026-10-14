Up until a few years ago, most Linux distributions relied on su for this purpose. su didn’t require the configuration that sudo required, and having a root account is traditional in Unix. This introduced a problem. Users were tempted to operate as root unnecessarily. In fact, some users operated their systems as the root user exclusively since it does away with all those annoying “permission denied” messages. This is how you reduce the security of a Linux system to that of a Windows system. Not a good idea.

When Ubuntu was introduced, its creators took a different tack. By default, Ubuntu disables logins to the root account (by failing to set a password for the account) and instead uses sudo to grant superuser privileges. The initial user account is granted full access to superuser privileges via sudo and may grant similar powers to subsequent user accounts.

# chown: Change File Owner and Group

The chown command is used to change the owner and group owner of a file or directory. Superuser privileges are required to use this command. The syntax of chown looks like this:

```
chown [owner][: [group]] file...
```

chown can change the file owner and/or the file group owner depending on the first argument of the command. Table 9-7 provides some examples.

Table 9-7: chown Argument Examples

| Argument | Results |
|---|---|
| bob | Changes the ownership of the file from its current owner to user bob. |
| bob:users | Changes the ownership of the file from its current owner to user bob and changes the file group owner to group users. |