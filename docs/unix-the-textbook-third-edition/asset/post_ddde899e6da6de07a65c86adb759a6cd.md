
```
echo " l:  To see the listing of files in your present working directory"
echo " w:  To see who's logged in"
echo " q:  To quit this program"
echo -n "Enter your option and hit <Enter>: "
read option
case "$option" in
    d)  date
        ;;
    l)  ls
        ;;
    w)  who
        ;;
    q)  exit 0
        ;;
esac
exit 0
$ ./case_demo
Use one of the following options:
    d:  To display today's date and present time
    l:  To see the listing of files in your present working directory
    w:  To see who's logged in
    q:  To quit this program
Enter your option and hit <Enter>: d
Sat Jul 26 17:28:19 PKT 2014
$ ./case_demo
Use one of the following options:
    d:  To display today's date and present time
    l:  To see the listing of files in your present working directory
    w:  To see who's logged in
    q:  To quit this program
Enter your option and hit <Enter>: w
malik            pts/0        Jul 15 08:11
davis            pts/1        Jul 27 16:11 (39.59.91.120)
sarwar           pts/2        Jul 27 16:48
jacob            pts/3        Jul 26 16:03
$ ./case_demo
Use one of the following options:
    d:  To display today's date and present time
    l:  To see the listing of files in your present working directory
    w:  To see who's logged in
    q:  To quit this program
Enter your option and hit <Enter>: a
$
```

From the output of the w option, it seems that davis is using the system through a remote login, most likely through an ssh session. Note that, when you enter a valid option, the expected output is displayed. However, when you enter input that is not a valid option (a in the preceding session), the program does not give you any feedback. The reason is that the case statement matches your input with all the patterns, one by one, and exits when there is no match. We need to modify the script slightly so that when you enter an invalid option, the script tells you so and then terminates. To do so we add the following code.

```
*) echo "Invalid option; try running the program again."
    exit 1
    ;;
```

We also enhance the script so that uppercase and lowercase inputs are considered to be the same. We use the pipe symbol (|) in the patterns to specify a logical OR operation. The enhanced code and some sample runs are shown in the following session.

```
$ cat case_demo
echo "Use one of the following options:"
echo "  d or D:    To display today's date and present time"
echo "  l or L:    To see the listing of files in your present working directory"
echo "  w or W:    To see who's logged in"
echo "  q or Q:    To quit this program"
echo -n "Enter your option and hit <Enter>: "
read option
case "$Option" in
    d|D)    date
            ;;
    l|L)    ls
            ;;
    w|W)    who
            ;;
    q|Q)    exit 0
            ;;
    *)      echo "Invalid option; try running the program again."
            exit 1
            ;;
esac
exit 0
$ ./case_demo
Use one of the following options:
    d or D:    To display today's date and present time
    l or L:    To see the listing of files in your present working directory
    w or W:    To see who's logged in
```

```
$ { date; echo -n "Hello, "; echo "world!"; }
Sat Aug  2 06:35:27 PKT 2014
Hello, world!
$ { date; echo -n "Hello, "; echo "world!"; } > groupout
$ more groupout
Sat Aug  2 06:35:40 PKT 2014
Hello, world!
$ { date; echo; ps; echo; echo "Hello, world!"; }
Sat Aug  2 06:36:39 PKT 2014
PID TT  STAT   TIME COMMAND
31078 1 Is   0:00.21 -csh (csh)
31113 1 S    0:00.05 /bin/sh
31371 1 R+   0:00.01 ps
Hello, world!
$ (date; pwd)
Sun Aug  3 12:47:24 PKT 2014
/home/sarwar
$ (date; pwd) > groupout
$ cat groupout
Sun Aug  3 12:52:42 PKT 2014
/home/sarwar
$ (date; echo; ps; echo; echo "Hello, world!")
Sat Aug  2 06:37:18 PKT 2014
PID TT  STAT   TIME COMMAND
31078 1 Is   0:00.21 -csh (csh)
31113 1 S    0:00.06 /bin/sh
31421 1 S+   0:00.00 /bin/sh
31423 1 R+   0:00.02 ps
Hello, world!
$
```

The outputs of the commands in this session are self-explanatory. Note that no child shell is created to execute the commands in { date; echo; ps; echo; echo "Hello, world!"; }. However, the commands in (date; echo; ps; echo; echo "Hello, world!") are executed under a child shell and the PID of the child shell is 31421.

## SUMMARY

Every UNIX shell has a programming language that allows you to write programs for performing tasks that cannot be performed by existing commands. These programs are commonly known as shell scripts. In its simplest form, a shell script consists of a list of shell commands that are executed by a shell one by one, sequentially. More advanced scripts contain program control flow statements for implementing multiway branching and repetitive execution of a block of commands in a script. The shell programs that consist of Bourne shell commands, statements, and features are called Bourne shell scripts.
