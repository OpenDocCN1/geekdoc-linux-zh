
| Command | Description |
| --- | --- |
| Talk | Talk to another user |
| write | Write message to another user |

# Programming Utilities

The following programming tools and languages are available based on which version of Unix you are using:

| Command | Description |
| --- | --- |
| dbx | Sun debugger |
| gdb | GNU debugger |
| make | Maintain program groups and compile programs. |
| nm | Print program’s name list |
| size | Print program’s sizes |
| strip | Remove symbol table and relocation bits |
| cb | C program beautifier |
| cc | ANSI C compiler for Suns SPARC systems |
| Ctrace | C program debugger |
| Gcc | GNU ANSI C Compiler |
| Indent | Indent and format C program source |
| Bc | Interactive arithmetic language processor |
| Gcl | GNU Common Lisp |
| Perl | General purpose language |
| Php | Web page embedded language |
| Py | Python language interpreter |
| Asp | Web page embedded language |
| CC | C++ compiler for Suns SPARC systems |
| g++ | GNU C++ Compiler |
| Javac | JAVA compiler |
| appletviewer | JAVA applet viewer |
| Netbeans | Java integrated development environment on Linux |
| Sqlplus | Run the Oracle SQL interpreter |
| Sqldir | Run the Oracle SQL data loader |
| MySql | Run the mysql SQL interpreter |

## Misc Commands

These commands list or alter system information.

| Command | Description |
| --- | --- |
| chfn | Change your finger information |
| chgrp | Change the group ownership of a file |
| chown | Change owner |
| date | Print the date |
| determin | Automatically find terminal type |
| du | Print amount of disk usage |
| echo | Echo arguments to the standard output |
| exit | Quit the system |
| finger | Print information about logged-in users |
| groupadd | Create a user group |
| groups | Show group memberships |
| homequota | Show quota and file usage |
| iostat | Report I/O statistics |
| kill | Send a signal to a process |
| last | Show last logins of users |
| logout | log off UNIX |
| lun | List user names or login ID |
| netstat | Show network status |
| passwd | Change user password |
| printenv | Display value of a shell variable |
| ps | Display the status of current processes |
| quota -v | Display disk usage and limits |
| reset | Reset terminal mode |
| script | Keep script of terminal session |
| setenv | Set environment variables |
| stty | Set terminal options |
| time | Time a command |
| top | Display all system processes |
| tset | Set terminal mode |
| tty | Print current terminal name |
| umask | Show the permissions that are given to view files by default |
| uname | Display name of the current system |
| uptime | Get the system up time |
| useradd | Create a user account |
| users | Print names of logged in users |
| vmstat | Report virtual memory statistics |
| w | Show what logged in users are doing |
| who | List logged in users |

# Chapter Seventeen: REGULAR EXPRESSION

A regular expression is a string that can be used to describe several sequences of characters. Regular expressions are used by several different Unix commands, including `ed`, `sed`, `awk`, `grep`, and, to a more limited extent, `vi`. Here `sed` stands for **stream editor** a stream oriented editor, which was created exclusively for executing scripts. Thus, all the input you feed into it passes through and goes to STDOUT and it does not change the input file.

## Invoking sed

Before we start, let us make sure you have a local copy of `/etc/passwd` text file to work with `sed`. As mentioned previously, `sed` can be invoked by sending data through a pipe to it as follows:

```
$ cat /etc/passwd | sed
Usage: sed [OPTION]... {script-other-script} [input-file]...

-n, --quiet, --silent
                 suppress automatic printing of pattern space
-e script, --expression=script
                 "..." 
```

The `cat` command dumps the contents of `/etc/passwd` to `sed` through the pipe into `sed`'s pattern space. The pattern space is the internal work buffer that `sed` uses to do its work.

## The sed General Syntax

General syntax for sed:

```
/pattern/action
```

Here, **pattern** is a regular expression, and **action** is one of the commands given in the following table. If **pattern** is omitted, **action** is performed for every line as we have seen above.

The slash characters ( / ) that surround the pattern are required because they are used as delimiters.

| Range | Description |
| :--- | :--- |
| P | Prints the line |
| D | Deletes the line |
| s/pattern1/pattern2/ | Substitutes the first occurrence of |

## Deleting All Lines with sed

Invoke `sed` again, but this time tell `sed` to use the editing command delete line, denoted by the single letter d:

```
$ cat /etc/passwd | sed ‘d’
$ 
```

Instead of invoking `sed` by sending a file to it through a pipe, you can instruct `sed` to read the data from a file, as in the following example. The following command does exactly the same thing as the previous example, without the cat command:

```
$ sed -e ‘d’ /etc/passwd
$ 
```

## The sed Addresses

`sed` also understands something called addresses. Addresses are either particular locations in a file or a range where a particular editing command should be applied. When `sed` encounters no addresses, it performs its operations on every line in the file.

The following command adds a basic address to the `sed` command you have been using:

```
$ cat /etc/passwd | sed ‘1d’ |more
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
$ 
```

Notice that the number 1 is added before the delete edit command. This tells `sed` to perform the editing command on the first line of the file. In this example, `sed` will delete the first line of /etc/passwd and print the rest of the file.

## The sed Address Ranges

So, what if you want to remove more than one line from a file? You can specify an address range with `sed` as follows:

```
$ cat /etc/passwd | sed ‘1, 5d’ |more
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
$
```

The above command will be applied on all the lines starting from 1 through 5. Therefore, it deletes the first five lines. Try out the following address ranges:

| Range | Description |
|---|---|
| `‘4,10d’` | Lines starting from 4th till 10th are deleted |
| `‘10,4d’` | Only 10th line is deleted, because sed does not work in reverse direction. |
| `‘4,+5d’` | This will match line 4 in the file, delete that line, continue to delete the next five lines, and then cease its deletion and print the rest |
| `‘2,5!d’` | This will delete everything except starting from 2nd till 5th line. |
| `‘1~3d’` | This deletes the first line, steps over the next three lines, and then deletes the fourth line. Sed continues applying this pattern until the end of the file. |
| `‘2~2d’` | This tells sed to delete the second line, step over the next line, delete the next line, and repeat until the end of the file is reached. |
| `‘4,10p’` | Lines starting from 4th till 10th are printed |
| `‘4,d’` | This would generate syntax error. |
| `‘,10d’` | This would also generate syntax error. |

**Note:** While using `p` action, you should use `-n` option to avoid repetition of line printing. Check the difference between these two commands:

```
$ cat /etc/passwd | sed -n ‘1,3p’
```

Check the above command without `-n` as follows:
