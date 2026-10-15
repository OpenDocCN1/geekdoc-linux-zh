

The ruptime command displays information about each system on your network. The information shows how each system has been performing. ruptime shows whether a system is up or down, how long it has been up or down, the number of users on the system, and the average load on the system for the last five, ten, and fifteen minutes.

```
$ ruptime
violet up 11+04:10, 8 users, load 1.20 1.10 1.00
garnet up 11+04:10, 20 users, load 1.50 1.40 1.30
```

## Remote Access Permission: .rhosts and .k5login

You use a .rhosts and .k5login (Kerberos) files to control access to your account by users using remote commands. Users create these files on their own accounts using a standard editor. They must be located in the user's home directory. In the next example, the user displays the contents of a .rhosts file:

```
$ cat .rhosts
garnet chris
violet robert
```

The .rhosts file is a simple way to allow other people access to your account without giving out your password. To deny access to a user, simply delete the system's name and the user's login name from your .rhosts file. If a user's login name and system are in an .rhosts file, that user can directly access that account without knowing the password (in place of using .rhosts, you could use a password). The .rhosts or .k5login files are required for other remote commands, such as remotely copying files or remotely executing Linux commands. The .k5login file will contain Kerberos names for users, including user names and realms. Such user will undergo Kerberos authentication to gain access.

The type of access .rhosts and .k5login provide enables you to use remote commands to access accounts directly that you might have on other systems. You do not have to log into them first. In effect, you can treat your accounts on other systems as extensions of the one you are currently logged into. Using the rcp command, you can copy any files from one directory to another no matter what account they are on. With the rsh command, you can execute any Linux command you want on any of your other accounts.

## rlogin, slogin, rcp, rsh, and ssh

You may have accounts on different systems in your network, or you may be permitted to access someone else's account on another system. You could access an account on another system by first logging into your own and then remotely logging in across your network to the account on the other system. You can perform such a remote login using the rlogin command, which takes as its argument a system name. The command connects you to the other system and begins login procedures. Bear in mind that if you are using an SSH-enabled network connection, you would use slogin instead of rlogin. The slogin command or Kerberos rlogin will provide secure encrypted login access.

The same is true for pipes. The first command (shown next) prints the list of files on the local system’s printer. The standard output is piped to your own line printer. In the second command, the list of files is printed on the remote system’s printer. The pipe is quoted and evaluated by the remote system, piping the standard output to the printer on the remote system.

```
$ ssh violet ls /home/robert | lpr
$ ssh violet ls /home/robert '|' lpr
```

> Note The Kerberos version of the remote commands also let you specify Kerberos realms and credentials.

| Remote Command | Effect |
|---|---|
| rwho | Displays all users logged into systems in your network. |
| ruptime | Displays information about each system on your network. |
| rlogin system-name | Allows you to log in remotely to an account on another system. |
| -l | Allows you to specify the login name of the account. |
| alogin system-name | Secure login to an account on another system. |
| rcp sys:name:file1 sys:name:file2 | Allows you to copy a file from an account on one system to an account on another system. With the -p option, preserves the modification times and modes of source files. |
| scp sys:name:file1 sys:name:file2 | Secure copy of a file from an account on one system to an account on another system. |
| rsh sys-name Linux-command | Allows you to remotely execute a command on another system. -l allows you to specify the login name. -n redirects input from the null special device, /dev/null. |
| ssh sys-name Linux-command | Secure remote execution of a command on another system. |

## TABLE 15-3 Remote Access Commands

