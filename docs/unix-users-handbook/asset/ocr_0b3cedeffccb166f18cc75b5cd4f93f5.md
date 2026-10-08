# NET HELP

**NET HELP** - Use this command to get help on any of the NET commands.

A commonly used option follows:

NET HELP command \| more This provides information about the *command* you specify.

The following example shows issuing the **NET HELP** command to get a list of commands for which help is available:

```
C:\ NET HELP
The syntax of this command is:
NET HELP_command
-or-
NET command /HELP
Commands available are:
NET ACCOUNTS      NET HELP          NET SHARE
NET COMPUTER      NET HELPMSG       NET START
NET CONFIG        NET LOCALGROUP    NET STATISTICS
NET CONFIG SERVER NET NAME          NET STOP
NET CONFIG WORKSTATION NET PAUSE    NET TIME
NET CONTINUE      NET PRINT         NET USE
NET FILE          NET SEND          NET USER
NET GROUP         NET SESSION       NET VIEW
NET HELP SERVICES lists the network services you can start.
NET HELP SYNTAX explains how to read NET HELP syntax lines.
NET HELP command \| MORE displays Help one screen at a time.
```

The following example shows issuing the **NET HELP** command to get information about the **NET GROUP** command:

```
C:\ NET HELP NET GROUP
The syntax of this command is:
NET GROUP  [groupname [//COMMENT:"text"]] [//DOMAIN]
          groupname [//ADD [//COMMENT:"text"] \| //DELETE]  [//DOMAIN]
          groupname username [...] [//ADD \| //DELETE] [//DOMAIN]
NET GROUP adds, displays, or modifies global groups on servers. Used
without parameters, it displays the groupnames on the server.
```