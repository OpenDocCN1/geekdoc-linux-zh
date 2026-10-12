TABLE 7.5 Control Switches for the /who Command

| Switch | Description |
| :--- | :--- |
| -away | Lists only users who are marked away. |
| -chops | Lists only channel operators. |
| -file filename | Lists only people who are listed in the file. |
| -here | Lists only users who are marked as here. |
| -host | Lists only users from the specified host. |
| -luusers | Lists only non-operators. |
| -name username | Lists only the users who have user ids that match the username argument. |
| -nick | Lists only users with matching nicknames. |
| -operators | Lists only operators. |
| -server | Lists only users from the specified server. |

# **whois**

Syntax:

/whois nicknames

This is used to get detailed information about users with the specified nicknames. You will get the following information about each user: user name, host, server, real name, and their away message. The real name has to be taken with a grain of salt because the user can set this to whatever he wants.

For example, you might get the following output if you try the following command:

```
/whois wsb.
*** wsb is wsb@test.gnulix.org (William B.)
*** on channels: @Gnulix
*** on irc via server irc-2.mit.edu (Massachusetts Institute of Technology)
*** wsb has been idle 27 seconds
```

# **whowas**

Syntax:

/whowas nickname

This shows detailed information about the user who last used the specified nickname. This will be shown even if the user is not logged in. You will be shown the same information as the /whois command outputs.