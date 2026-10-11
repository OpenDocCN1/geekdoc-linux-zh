uucp:*:4:8:/var/spool/uucppublic:
news:*:6:6:/var/spool/news:/bin/csh
sync:*:11::/bin/sync
ellie:aVD17T88mBMfGy:9496:40:Ellie Shellie:/home/jody/ellie:/bin/ksh

# Windows.  Windows stores information about users in a binary database called SAM (Security Accounts Manager), part of the Registry. Because the data is stored in binary format, normal Pei Read operations won't work. It is better to use the Win32 extensions to get user information. Win32.NetAdmin is bundled with ActiveState under *per\site\lib\win32. (See Table 16-9.) You can manipulate a user account with two functions of this module: UserGetAttributes and UserSetAttributes.

The Win 32 net.exe command also displays information about the user and the system.

# EXAMPLE 16.38

```
    1. C:\ net help
        The syntax of this command is:

        NET HELP command
            -or-
        NET command /HELP

        Commands available are:
        NET ACCOUNTS      NET HELP      NET SHARE
        NET COMPUTER      NET HC\ELPMSG   NET START
        NET CONFIG        NET LOCALGROUP  NET STATISTICS
        NET CONFIG SERVER NET NAME        NET STOP
        NET CONFIG WORKSTATION NET PAUSE   NET TIME
        NET CONTINUE      NET PRINT       NET USER
        NET FILE          NET SEND        NET VIEW
        NET GROUP         NET SESSION

        NET HELP SERVICES lists the network services you can start.
        NET HELP SYNTAX explains how to read NET HELP syntax lines.
        NET HELP command | MORE displays Help one screen at a time.

    2. C:\ net user

        User accounts for \HOMEBOUND

        Administrator    Ellie Quigley    Guest.
        The command completed successfully.
```