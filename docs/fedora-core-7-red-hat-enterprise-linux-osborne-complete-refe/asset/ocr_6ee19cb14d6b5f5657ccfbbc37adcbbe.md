```
printable = yes
printer = myhp
oplocks = no
share modes = no
printing = cups
```

As with shares, you can restrict printer use to certain users, denying it to public access. The following example sets up a printer accessible only by the users laris a and aleina (you could add other users if you want). Users need to have write access to the printer’s spool directory.

```
[larisalaser]
    path = /var/spool/samba
    read only = no
    valid users = laris a aleina
    guest ok = no
    printable = yes
    printing = cups
    printer = larisalaser
    oplocks = no
    share modes = no
```

# Variable Substitutions

For string values assigned to parameters, you can incorporate substitution operators. This provides greater flexibility in designating values that may be context-dependent, such as usernames. For example, suppose a service needs to use a separate directory for each user who logs in. The path for such directories could be specified using the %u variable that substitutes in the name of the current user. The string path = /tmp/%u would become path = /tmp/justin for the justin user and /tmp/dylan for the dylan user. Table 39-3 lists several of the more common substitution variables.

| Variable | Description |
| :------- | :---------- |
| %$ | Name of the current service |
| %P | Root directory of the current service |
| %u | Username of the current service |
| %H | Home directory of the user |
| %h | Internet hostname on which Samba is running |
| %m | NetBIOS name of the client machine |
| %L | NetBIOS name of the server |
| %M | Internet name of the client machine |
| %I | IP address of the client machine |

TABLE 39-3  Samba Substitution Variables