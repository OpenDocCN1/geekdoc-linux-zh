# Using Variables

Just running individual commands from the shell script is useful, but this has its limitations. Often you'll want to incorporate other data in your shell commands to process information. You can do this by using variables. Variables allow you to temporarily store information within the shell script for use with other commands in the script. This section shows how to use variables in your shell scripts.

# Environment variables

You've already seen one type of Linux variable in action. Chapter 5 described the environment variables in the Linux system. You can access these values from your shell scripts as well.

The shell maintains environment variables that track specific system information, such as the name of the system, the name of the user logged in to the system, the user's system ID (called UID), the default home directory of the user, and the search path used by the shell to find programs. You can display a complete list of active environment variables by using the set command:

```
$ set
BACKSPACE=Delete
BASH=/bin/bash
EID=1000
HISTFILE=/home/rich/.bash_history
HISTFILESIZE=1000
HISTSIZE=1000
HOME=/home/rich
HOSTNAME=testing
HOSTTYPE=i586
LANG=en
LANGUAGE=en_US
LINES=24
LOGNAME=rich
```

You can tap into these environment variables from within your scripts by using the variable's name preceded by a dollar sign. This is demonstrated in the following script:

```
$ cat test2
!/bin/bash
# display user information from the system.
echo "User info for userid: $USER"
echo UID: $UID
echo HOME: $HOME
$
```