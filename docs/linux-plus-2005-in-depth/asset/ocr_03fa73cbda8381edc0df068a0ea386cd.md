| |Table 5-3|Common criteria used with the find command (Continued)| | | |
| --- | --- | --- | --- | --- | --- |
|Criteria|Description| | | |
| **-type x**|Searches for files of type x where x is:| | | |
|◊ b for block files| | | |
|◊ c for character files| | | |
|◊ d for directory files| | | |
|◊ p for named pipes| | | |
|◊ f for regular files| | | |
|◊ l for symbolic links (shortcuts)| | | |
|◊ s for sockets| | | |
| **-user x**|Searches for files owned by a certain user or UID (x)| | | |

Although the *find* command can be used to search for files based on many criteria, it might take several minutes to complete the search if the number of directories and files being searched is large. To reduce the time needed to search, narrow down the directories searched by specifying a subdirectory when possible. It takes less time to search the /usr/local/bin directory and its subdirectories, compared to searching the /usr directory and all of its subdirectories. As well, if the filename that we are searching for is an executable file, that file can likely be found in less time using the **which** command. The *which* command only searches directories that are listed in a special variable called the **PATH** variable in the current BASH shell. Before exploring the *which* command, you must understand the usage of PATH.

Executable files can be stored in directories scattered around the directory tree. Recall from FHS that most executable files are stored in directories named bin or sbin, yet there are over 20 bin and sbin directories scattered around the directory tree after a typical Red Hat Linux installation. To ensure that users do not need to specify the full pathname to commands such as *ls* (which is the executable file /bin/ls), there exists a special variable called **PATH** that is placed into memory each time a user logs in to the Linux system. Recall that you can see the contents of a certain variable in memory by using the $ metacharacter with the *echo* command:

```
[root@server1 root]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:
/usr/bin:/usr/X11R6/bin:/root/bin
[root@server1 root]# _
```

The **PATH** variable lists directories that are searched for executable files if a relative or absolute pathname was not specified when executing a command on the command line. In the preceding output, when a user types the *ls* command on the command line and presses Enter, the system recognizes that the command was not an absolute pathname (for example, /bin/ls) or relative pathname (for example, ../bin/ls) and then proceeds to look for the *ls* executable file in the /usr/kerberos/sbin directory, then the /usr/kerberos/bin directory, then the /usr/local/sbin