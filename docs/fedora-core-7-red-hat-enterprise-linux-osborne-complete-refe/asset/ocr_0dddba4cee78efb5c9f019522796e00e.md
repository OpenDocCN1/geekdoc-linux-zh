place of using .k5login, you could use a password). The .k5login file will contain Kerberos names for users, including user names and realms. Such a user will undergo Kerberos authentication to gain access. A .k5login file is required for other remote commands, such as remotely copying files or remotely executing Linux commands.

The type of access .k5login provides enables you to use remote commands to directly access accounts that you might have on other systems. You do not have to log in to them first. In effect, you can treat your accounts on other systems as extensions of the one you are currently logged in to. Using the rcp command, you can copy any files from one directory to another no matter which of your accounts they are on. With the rsh command, you can execute any Linux command you want on any of your other accounts.

# rlogin, slogin, rcp, scp, rsh, and ssh

You may have accounts on different systems in your network, or you may be permitted to access someone else’s account on another system. You could access an account on another system by first logging in to your own account, and then remotely logging in across your network to the account on the other system. You can perform such a remote login using the rlogin command, which takes as its argument a system name. The command connects you to the other system and begins login procedures. Bear in mind that if you are using an SSH-enabled network connection, you could use slogin instead of rlogin. Either slogin or Kerberos rlogin will provide secure encrypted login access.

You can use the rcp command to copy files to and from remote and local systems. For SSH-enabled network connections, you would use scp instead of rcp. The rcp and scp commands are file transfer tools that operate like the cp command, but across a network connection to a remote system. The rcp command begins with the keyword rcp and has as its arguments the names of the source file and the copy file. To specify the file on the remote system, you need to place the remote system name before the filename, separated from it by a colon. When you are copying a file on the remote system to your own, the source file is a remote file and requires the remote system’s name. The copy file is a file on your own system and does not require a system name:

```
$ rcp remote-system-name:source-file copy-file
```

In the next example, the user copies the file wednesday from the remote system violet to her own system and renames the file today:

```
$ rcp violet:wednesday today
```

You can also use scp or rcp to copy whole directories to or from a remote system. The scp command with the -r option copies a directory and all its subdirectories from one system to another. Like the cp command, these commands require source and destination directories. The directory on the remote system requires that the system name and colon be placed before the directory name. When you copy a directory from your own system to a remote system, the copy directory is on the remote system and requires the remote system’s name. In the next example, the user uses the scp command to copy the directory letters to the directory oldnotes on the remote system violet:

```
$ scp -r letters violet:oldnotes
```