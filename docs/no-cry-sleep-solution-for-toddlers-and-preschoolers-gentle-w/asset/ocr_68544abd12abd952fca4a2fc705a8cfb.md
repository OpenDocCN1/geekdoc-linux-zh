name. Sometimes the login name on the remote system is the same as the login name on your own system. If the names are the same, press ENTER at the prompt. If they are different, enter the remote system’s login name. After entering the login name, you are prompted for the password. In the next example, the user connects to the remote system garnet and logs into the robert account:

```
$ ftp
ftp> open
(to) garnet
Connected to garnet.berkeley.edu.
220 garnet.berkeley.edu FTP server ready.
Name (garnet.berkeley.edu:root): robert
Password:
user robert logged in
ftp>
```

Once logged in, you can execute Linux commands on either the remote system or your local system. You execute a command on your local system in ftp by preceding the command with an exclamation point. Any Linux commands without an exclamation point are executed on the remote system. One exception exists to this rule. Whereas you can change directories on the remote system with the cd command, to change directories on your local system, you need to use a special ftp command called lcd (local cd). In the next example, the first command lists files in the remote system, while the second command lists files in the local system:

```
ftp> ls
ftp> !ls
```

The ftp program provides a basic set of commands for managing files and directories on your remote site, provided you have the permission to do so (see Table 14-8). You can use

| Command | Effect |
|---|---|
| ftp | Invokes the ftp program |
| open site-address | Opens a connection to another system |
| close | Closes connection to a system |
| quit or bye | Ends ftp session |
| ls | Lists the contents of a directory |
| dir | Lists the contents of a directory in long form |
| get filename | Sends file from remote system to local system |
| put filename | Sends file from local system to remote system |
| mget regular-expression | Enables you to download several files at once from a remote system. You can use special characters to specify the files; you are prompted to transfer each file in turn |