# The getopts Command 183

```
if [ "mailopt" = FALSE ]
then
    echo "$user has logged on"
else
    runner=$(who am i | cut -cl-8)
    echo "$user has logged on" | mail runner
fi
```

```
$ waitfor -m
```

Missing user name!

```
$ waitfor -x fred
waitfor: illegal option -- x
Usage: waitfor [-m] [-t n] user
-m means to be informed by mail
-t means check every n secs
```

Illegal option

```
$ waitfor -m -t 600 &
[1] 5792
```

Check every 10 min. for ann

Let's look at the last line closely. When the line

```
waitfor -t 600 &
```

is executing, the following occurs inside the loop: getopts is invoked and stores the character m inside the variable option, sets OPTIND to 2, and returns a zero status.

The case command determines what was stored inside option. A match on the character m indicates that the "send mail" option was selected, so mailopt is set to TRUE. (Note that the ? inside the case is quoted. This is to remove its special meaning as a pattern matching from the shell.)

The second time getopts is executed, getopts stores the character i option, stores the next command line argument (600) inside OPTARG, sets OPTIND to 3, and returns a zero exit status. The case command matches the character t inside option. The code associated with that case copies the value of 600 that was stored in OPTARG in the interval.

The third time getopts is executed, getopts returns a nonzero exit status, indicating that it reached the end of the user-specified command options.

The program checks the value of OPTIND against $$ to make sure that a username was typed on the command line. If OPTIND is greater than $$, no more arguments remain and the user forgot the user name argument. Otherwise, the shift command is used to move the user name argument into $1. The actual number of places to shift is one less than the value of OPTIND.