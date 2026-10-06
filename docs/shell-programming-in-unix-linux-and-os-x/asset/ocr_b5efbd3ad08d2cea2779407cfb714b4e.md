146      Chapter 7 Decisions, Decisions

Who's on?

```
$ who
root      console Jul 8 10:37
barney    tty03      Jul 8 12:38
fred      tty04      Jul 8 13:40
joanne    tty07      Jul 8 09:35
tony      tty19      Jul 8 08:30
lulu      tty23      Jul 8 09:55
$ on pat
pat is not logged on
$ on tony
tony is logged on
$
```

To turn a quick prototype into a useful program for the long term, it's a good practice to make sure that the correct number of arguments is passed to the program. If the user specifies the wrong number of arguments, an appropriate error message can be issued, along with a usage message. Like this:

```
$ cat on
#
# determine if someone is logged on -- version 4
#

# see if the correct number of arguments were supplied
#
if [ "$#" -ne 1 ]
then
    echo "Incorrect number of arguments"
    echo "Usage: on user"
else
    user="$1"

    if who | grep "$user" >/dev/null
    then
        echo "$user is logged on"
    else
        echo "$user is not logged on"
    fi
fi
```

It seems like a lot of changes, but without wrapping all the previous code within an else-fi pair, the primary addition is an if command to evaluate whether the correct number of arguments were supplied. If $$ is not equal to 1, the required number of arguments, the program prints two error messages; otherwise, the commands after the else clause are executed. Note that two fi commands are required because if commands are used.