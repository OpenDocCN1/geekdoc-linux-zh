# Shell Variables

the current directory needs to be identified. The following output demonstrates how this variable works:

```
```
[root@server1 ~]# pwd
/root
[root@server1 ~]# echo $PWD
/root
[root@server1 ~]# cd /etc
[root@server1 etc]# pwd
/etc
[root@server1 ~]# echo $PWD
/etc
[root@server1 ~]#
```
```

The PATH variable is one of the most important variables in the BASH shell, as it allows users to execute commands by typing the command name alone. Recall that most commands are represented by an executable file on the hard drive. These executables are typically stored in directories named bin or sbin in various locations throughout the Linux directory tree. To execute the *ls* command, you could either type the absolute or relative pathname to the file (that is, */usr/bin/ls* or *./usr/bin/ls*) or simply type the letters “ls” and allow the system to search the directories listed in the PATH variable for a command named *ls*. Sample contents of the PATH variable are shown in the following output:

```
```
[root@server1 ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
[root@server1 ~]#
```
```

In this example, if the user had typed the command *ls* at the command prompt and pressed Enter, the shell would have noticed the lack of a / character in the pathname and proceeded to search for the file *ls* in the */usr/local/bin* directory, then the */usr/local/bin* directory, the */usr/sbin* directory, and then the */usr/bin* directory before finding the *ls* executable file. If no file is found in any directory in the PATH variable, the shell returns an error message, as shown here with a misspelled command and any similar command suggestions:

```
```
[root@server1 ~]# lss
bash: lss: command not found...
[Similar command is: 'ls']
[root@server1 ~]#
```
```

Thus, if a command is located within a directory that is listed in the PATH variable, you can simply type the name of the command on the command line to execute it. The shell will then find the appropriate executable file on the filesystem. All of the commands used in this book so far have been located in directories listed in the PATH variable. However, if the executable file is not in a directory listed in the PATH variable, the user must specify either the absolute or relative pathname to the executable file. The following example uses the myprogram file in the /root directory (a directory that is not listed in the PATH variable):

```
```
[root@server1 ~]# pwd
/root
[root@server1 ~]# ls -F
Desktop/ myprogram*
[root@server1 ~]# myprogram
bash: myprogram: command not found...
```
```