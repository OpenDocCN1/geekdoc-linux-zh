
## Linux Hack

testing: var/log/anaconda.syslog

skip...

testing: var/log/wtmp

testing: var/log/wtmp.1

testing: var/log/Xorg.0.log

Ajay Kumar Tiwari

OK

OK

OK

OK

No errors detected in compressed data of var-log.zip.

## Hack 48. Tar Command Basics

tar command (tape archive) is used to convert a group of files into an archive.

Syntax: tar [options] [tar-archive-name] [other-file-names]

How can I create a single backup file of all files and subdirectories under my home directory?

The following command creates a single archive backup file called my_home_directory.tar under /tmp. This archive will contain all the files and subdirectories under /home/jsmith.

- Option c, stands for create an archive.
- Option v stands for verbose mode, displays additional information while executing the command.
- Option f indicates the archive file name mentioned in the command.

```
# tar cvf /tmp/my_home_directory.tar /home/jsmith
```

67

## Linux Hack

Ajay Kumar Tiwari

### How do I view all the files inside the tar archive?

Option t will display all the files from the tar archive.

```
# tar tvf /tmp/my_home_directory.tar
```

### How do I extract all the files from a tar archive?

Option x will extract the files from the tar archive as shown below. This will extract the content to the current directory location from where the command is executed.

```
# tar xvf /tmp/my_home_directory.tar
```

### How do I extract tar.gz files to a specific directory?

```
# tar xvfz /tmp/my_home_directory.tar.gz -C /home/ramesh
```

## Hack 49. Combine gzip, bzip2 with tar

### How to use gzip with tar?

Add option z to the tar command when dealing with tar.gz compressed file.

```
# tar cvfz /tmp/my_home_directory.tar.gz /home/jsmith
```

```
# tar xvfz /tmp/my_home_directory.tar.gz
```

```
# tar tvfz /tmp/my_home_directory.tar.gz
```

Note: Using gzip is faster when compared to bzip2.

## Linux Hack

Ajay Kumar Tiwari

### How to use bzip2 with tar?

Add option j to the tar command when dealing with tar.bz2 compressed file.

```
# tar cvfj /tmp/my_home_directory.tar.bz2 /home/jsmith
# tar xvfj /tmp/my_home_directory.tar.bz2
# tar tvfj /tmp/my_home_directory.tar.bz2
```

Note: Using bzip2 gives higher level of compression when compared to gzip.

## Linux Hack

Ajay Kumar Tiwari

## Chapter 8: Command Line History

When you are using Linux command line frequently, using the history effectively can be a major productivity boost. In fact, once you have mastered the 15 examples that I’ve provided here, you’ll find using command line more enjoyable and fun.

### Hack 50. Display TIMESTAMP in history using HISTTIMEFORMAT

Typically when you type history from command line, it displays the command # and the command. For auditing purpose, it may be beneficial to display the timestamp along with the command as shown below.

```
# export HISTTIMEFORMAT='%F %T '
# history
1
2
3
4
| more
2008-08-05
2008-08-05
2008-08-05
2008-08-05
19:02:39
19:02:39
19:02:39
19:02:39
service network restart
exit
id
```

```
cat /etc/redhat-release
```

Note: You can also setup the following alias to view the recent history commands.

```
alias h1='history 10'
```

```
alias h2='history 20'
```

```
alias h3='history 30'
```

### Hack 51. Search the history using Control+R

I strongly believe that this may be your most frequently used feature of history. When you’ve already executed a very long command, you can simply search history using a keyword and re-execute the same command without having to type it fully. Press Control+R and type the keyword.

In the following example, I searched for red, which displayed the previous command “cat /etc/redhat-release” in the history that contained the word red.

### Note: Press Ctrl+R from the command prompt, which will display the reverse-i-search prompt as shown below

```
(reverse-i-search)`red': cat /etc/redhat-release
```

### Note: Press enter when you see your command, which will execute the command from the history

```
# cat /etc/redhat-release
```

Fedora release 9 (Sulphur)

Sometimes you want to edit a command from history before executing it. For e.g. you can search for httpd, which will display service httpd stop from the command history, select this command and change the stop to start and re-execute it again as shown below.

### Note: Press Ctrl+R from the command prompt, which will display the reverse-i-search prompt

```
(reverse-i-search)`httpd': service httpd stop
```

### Note: Press either left arrow or right arrow key when you see your command, which will display the command for you to edit, before executing it

```
# service httpd start
```

## Linux Hack

Ajay Kumar Tiwari

### Hack 52. Repeat previous command quickly using 4 different methods

Sometime you may end up repeating the previous commands for various reasons. Following are the 4 different ways to repeat the last executed command.

- 1. Use the up arrow to view the previous command and press enter to execute it.
- 2. Type !! and press enter from the command line
- 3. Type !-1 and press enter from the command line.
- 4. Press Control+P will display the previous command, press enter to execute it

## Linux Hack

Ajay Kumar Tiwari

### Hack 53. Execute a specific command from history

In the following example, If you want to repeat the command #4, execute !4 as shown below.

```
# history
1
2
3
4
| more
service network restart
exit
id
cat /etc/redhat-release
# !4
cat /etc/redhat-release
Fedora release 9 (Sulphur)
```

## Linux Hack

Ajay Kumar Tiwari

### Hack 54. Execute previous command that starts with a specific word

Type ! followed by the starting few letters of the command that you would like to re-execute. In the following example, typing !ps and enter, executed the previous command starting with ps, which is 'ps aux | grep yp'.

```
# !ps
ps aux | grep yp
  root16947 0.0
Sl13:100:00 ypbinding
  root17503 0.0
S+19:190:00 grep yp
0.1
0.0
36516
4124
1264 ?
740 pts/0
```

### Hack 55. Control the total number of lines in the history using HISTSIZE

Append the following two lines to the .bash_profile and relogin to the bash shell again to see the change. In this example, only 450 command will be stored in the bash history.

```
# vi ~/.bash_profile
HISTSIZE=450
HISTFILESIZE=450
```

### Hack 56. Change the history file name using HISTFILE

By default, history is stored in ~/.bash_history file. Add the following line to the .bash_profile and relogin to the bash shell, to store the history command in .commandline_warrior file instead of .bash_history file. I’m yet to figure out a practical use for this. I can see this getting used when you want to track commands executed from different terminals using different history file name.

```
# vi ~/.bash_profile
HISTFILE=/root/.commandline_warrior
```

### Hack 57. Eliminate the continuous repeated entry from history using HISTCONTROL

In the following example pwd was typed three times, when you do history, you can see all the 3 continuous occurrences of it. To eliminate duplicates, set HISTCONTROL to ignoredups as shown below.

```
# pwd
# pwd
# pwd
# history | tail -4
  44 pwd
  45 pwd
  46 pwd
  47 history | tail -4
```

[Note: There are three pwd commands in history, after executing pwd 3 times as shown above]

```
# export HISTCONTROL=ignoredups
# pwd
# pwd
# pwd
# history | tail -3
  56 export HISTCONTROL=ignoredups
  57 pwd
  58 history | tail -4
```

## Linux Hack

Ajay Kumar Tiwari

[Note: There is only one pwd command in the history, even after executing pwd 3 times as shown above]

### Hack 58. Erase duplicates across the whole history using HISTCONTROL

The ignoredups shown above removes duplicates only if they are consecutive commands. To eliminate duplicates across the whole history, set the HISTCONTROL to erasedups as shown below.

```
# export HISTCONTROL=erasedups
# pwd
# service httpd stop
# history | tail -3
  38 pwd
  39 service httpd stop
  40 history | tail -3
# ls -ltr
# service httpd stop
# history | tail -6
  35 export HISTCONTROL=erasedups
  36 pwd
  37 history | tail -3
  38 ls -ltr
  39 service httpd stop
  40 history | tail -6
```

[Note: The previous service httpd stop after pwd got erased]
