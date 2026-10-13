
![](img/32a48d8db4c23e6e2eb70d1e5034c976_350_0.png)

## RSH, Kerberos, and SSH Remote Access Commands

The remote access commands were designed for smaller networks, such as intranets. They enable you to log in remotely to another account on another system and to copy files from one system to another. You can also obtain information about another system, such as who is logged on currently (see Table 15-3). Many of the remote commands have comparable network communication utilities used for the Internet. For example, rlogin, which remotely logs into a system, is similar to telnet. The rcp command, which remotely copies files, performs much the same function as ftp.

There are security risks with the use of remote operations like rcp, rlogin, and rsh (RSH package). Such commands allow easy unencrypted remote access to a Linux system. These commands should be used only within a local secure network. For Internet operations like these, you should use the secure versions of these commands provided by Kerberos and the Secure Shell (SSH), such as ssh, slogin, or scp (see Chapter 18). SSH commands are encrypted, providing a much higher level of security. Kerberos provides versions for Telnet, rlogin, rcp, rsh, and ftp, which provide authentication and encryption. The Kerberos versions operate using the same commands and options as the originals, making their use transparent to the user. If you install Kerberos on your system, Red Hat configures the user PATH variable to access the Kerberos versions of the remote commands, located at /usr/kerberos/bin, instead of /usr/bin.

You can use several commands to obtain information about different systems on your network. You can find out who is logged in, get information about a user on another system, or find out if a system is up and running. For example, the rwho command functions in the same way as the who command. It displays all the users currently logged into each system in your network.

```
$ rwho
violet robert:tty1 Sept 10 10:34
garnet chris:tty2 Sept 10 09:22
```

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

Your accounts on other systems as extensions of the one you are currently logged into. Using the rcp command, you can copy any files from one directory to another no matter what account they are on. With the rsh command, you can execute any Linux command you want on any of your other accounts.

## rlogin, slogin, rcp, scp, rsh, and ssh

You may have accounts on different systems in your network, or you may be permitted to access someone else's account on another system. You could access an account on another system by first logging into your own and then remotely logging in across your network to the account on the other system. You can perform such a remote login using the rlogin command, which takes as its argument a system name. The command connects you to the other system and begins login procedures. Bear in mind that if you are using an SSH-enabled network connection, you would use slogin instead of rlogin. The slogin command or Kerberos rlogin will provide secure encrypted login access.

You can use the rcp command to copy files to and from remote and local systems. For SSH-enabled network connections, you would use scp instead of rcp. rcp and scp are file transfer tools that operate like the cp command, but across a network connection to a remote system. The rcp command requires the remote system to have your user name and login name in its .rhosts file. The rcp command begins with the keyword rcp and has as its arguments the names of the source file and the copy file. To specify the file on the remote system, you need to place the remote system name before the filename, separated by a colon. When you are copying a file on the remote system to your own, the source file is a remote file and requires the remote system's name. The copy file is a file on your own system and does not require a system name:

```
$ rcp remote-system-name:source-file copy-file
```

In the next example, the user copies the file wednesday from the remote system violet to her own system and renames the file today:

```
$ rcp violet:wednesday today
```

You can also use scp or rcp to copy whole directories to or from a remote system. The scp command with the -r option copies a directory and all its subdirectories from one system to another. Like the cp command, these commands require source and copy directories. The directory on the remote system requires that the system name and colon be placed before the directory name. When you copy a directory from your own system to a remote system, the copy directory is on the remote system and requires the remote system's name. In the next example, the user uses the scp command to copy the directory letters to the directory oldnotes on the remote system violet:

```
$ scp -r letters violet:oldnotes
```

At times, you may need to execute a single command on a remote system. The rsh command executes a Linux command on another system and displays the results on your own. Your system name and login name must, of course, be in the remote system's .rhosts file. For SSH-enabled network connections, you would use ssh instead of rsh. The ssh and rsh commands take two general arguments: a system name and a Linux command. The syntax is as follows:

```
$ rsh remote-system-name Linux-command
```

In the next example, the rsh command executes an ls command on the remote system violet to list the files in the /home/robert directory on violet:

```
$ rsh violet ls /home/robert
```

Special characters are evaluated by the local system unless quoted. If you quote a special character, it becomes part of the Linux command evaluated on the remote system. Quoting redirection operators enables you to perform redirection operations on the remote system. In the next example, the redirection operator is quoted. It becomes part of the Linux command, including its argument, the filename myfiles. The ls command then generates a list of filenames that is redirected on the remote system to a file called myfiles, also located on the remote system.

```
$ ssh violet ls /home/robert '>' myfiles
```

The same is true for pipes. The first command (shown next) prints the list of files on the local system's printer. The standard output is piped to your own line printer. In the second command, the list of files is printed on the remote system's printer. The pipe is quoted and evaluated by the remote system, piping the standard output to the printer on the remote system.

```
$ ssh violet ls /home/robert | lpr
$ ssh violet ls /home/robert '|' lpr
```

Note that Kerberos version of the remote commands also let you specify Kerberos realm and credentials.

### Table 15-3: Remote Access Commands

| Remote Command | Effect |
|---|---|
| rwho | Displays all users logged into systems in your network. |
| ruptime | Displays information about each system on your network. |
| rlogin system-name | Allows you to log in remotely to an account on another system.
-l Allows you to specify the login name of the account. |
| slogin system-name | Secure login to an account on another system. |
