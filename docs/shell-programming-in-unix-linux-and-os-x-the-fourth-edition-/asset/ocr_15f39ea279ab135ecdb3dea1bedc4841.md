```
```sh
if [ "$mailopt" = FALSE]
then
        echo "$user has logged on"
else
        runner=$(who am i | cut -c1-8)
        echo "$user has logged on" | mail $runner
fi
```
```

```
```sh
$ waitfor -m
Missing user name!
$ waitfor -x fred                    Illegal option
waitfor: Illegal option -- x
Usage: waitfor [-m] [-t n] user
    -m means to be informed by mail
    -t means check every n secs.
$ waitfor -m -t 600 ann &
[1] 5792
$
```
```

Check every 10 min. for ann

Let’s look at the last line more closely. When the line

```
```sh
waitfor -m -t 600 ann &
```
```

is executed, the following occurs inside the while loop: getopts is invoked and stores the character m inside the variable option, sets OPTIND to 2, and returns a zero exit status.

The case command then determines what was stored inside option. A match on the character m indicates that the “send mail” option was selected, so mailopt is set to TRUE. (Note that the ? inside the case is quoted. This is to remove its special meaning as a pattern matching character from the shell.)

The second time getopts is executed, getopts stores the character t inside option, stores the next command line argument (600) inside OPTARG, sets OPTIND to 3, and returns a zero exit status. The case command then matches the character t stored inside option. Then the code associated with that case copies the value of 600 that was stored in OPTARG into the variable interval.

The third time getopts is executed, getopts returns a nonzero exit status, indicating that it’s reached the end of the user-specified command options.

The program then checks the value of OPTIND against $# to make sure that a username was typed on the command line. If OPTIND is greater than $#, then no more arguments remain and the user forgot the username argument. Otherwise, the shift command is used to move the user name argument into $1. The actual number of places to shift is one less than the value of OPTIND.