+   10. From a Windows command prompt, use **net view** to display a list of shares available from the server (\textbf{plum} in this example):

```
```
C:\>net view \\plum

Shared resources at \\plum

Samba Server Version 4.0.6

Share name   Type   Used as Comment

sam          Disk   Home Directories
tmp          Disk   Temporary Directory

The command completed successfully.
```
```

+   11. Try to map (mount) the drive from a Windows command prompt. The following command attempts to mount the share named **sam** on **plum** as drive **X:**

```
```
C:\>net use x: \\plum\sam

Enter the user name for 'plum': sam
Enter the password for plum:

The command completed successfully.
```
```

+   12. From the Samba server, use **nmblookup** (*samba-client* package) to query the nmbd server, using the special name **\_\_SAMBA\_\_** for the server's NetBIOS name. The **-d 2** option turns the debugger on at level 2, which generates a moderate amount of output. The **-B** option specifies the server you are querying.

```
```
$ nmblookup -d 2 -B 127.0.0.1 __SAMBA__
...
Querying __SAMBA__ on 127.0.0.1
Got a positive name query response from 127.0.0.1 ( 192.168.206.181 )
192.168.206.181 __SAMBA__<00>
```
```

The next example uses **nmblookup**, without setting the debug level, to query the local system for all NetBIOS names.

```
```
$ nmblookup -B 127.0.0.1 \
querying * on 127.0.0.1 <00>
192.168.206.181 *<00>
```
```

To query for the master browser from the local server, run **nmblookup** with the **-A** option followed **localhost** or the name of the server:

```
```
$ nmblookup -A 127.0.0.1
Looking up status of 127.0.0.1
PLUM <00> - B <ACTIVE>
PLUM <03> - B <ACTIVE>
PLUM <20> - B <ACTIVE>
MCS <00> - <GROUP> B <ACTIVE>
MCS <1e> - <GROUP> B <ACTIVE>

MAC Address = 00-00-00-00-00-00
```
```