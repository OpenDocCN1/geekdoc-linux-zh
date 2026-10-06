
You can add echo statements anywhere in your shell scripts where you need to display additional information:

```bash
$ cat test1
#!/bin/bash
# This script displays the date and who's logged on
echo "The time and date are: "
date
echo "Let's see who's logged into the system"
who
```

When you run this script, it produces the output:

```bash
$ chmod u+x test1
./test1
The time and date are:
Mon Sep 24 20:09:35 EST 2007
Let's see who's logged into the system:
rich :0 2007-09-24 18:23 (console)
rich pts/1 2007-09-24 18:24
rich pts/0 2007-09-24 18:42
barbara pts/2 2007-09-24 19:30
katie pts/3 2007-09-24 19:39
$
```

That's nice, but what if you want to echo a text string on the same line as a command output? You can use the -n for the echo statement to do that. Just change the first echo statement line to:

```bash
echo -n "The time and date are: "
```

You'll need to use quotes around the string to ensure there's a space at the end of the echoed string. The command output begins exactly where the string stops. The output will look like:

```bash
$ ./test1
The time and date are: Mon Sep 24 20:11:35 EST 2007
Let's see who's logged into the system:
rich :0 2007-09-24 18:23 (console)
rich pts/1 2007-09-24 18:24
rich pts/0 2007-09-24 18:42
barbara pts/2 2007-09-24 19:30
katie pts/3 2007-09-24 19:39
$
```

Perfect! The echo command is a crucial piece of shell scripts that interact with users. You'll find yourself using it in many situations, especially when you want to display the values of script variables. Let's look at that.

## Using Variables

Just running individual commands from the shell script is useful, but this has its limitations. Often you'll want to incorporate other data in your shell commands to process information. You can do this by using variables. Variables allow you to temporarily store information within the shell script for use with other commands in the script. This section shows how to use variables in your shell scripts.

## Environment variables

You've already seen one type of Linux variable in action. Chapter 5 described the environment variables in the Linux system. You can access these values from your shell scripts as well.

The shell maintains environment variables that track specific system information, such as the name of the system, the name of the user logged in to the system, the user's system ID (called UID), the default home directory of the user, and the search path used by the shell to find programs. You can display a complete list of active environment variables by using the set command:

```bash
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

```bash
$ cat test2
#!/bin/bash
# display user information from the system.
echo "User info for userid: $USER"
echo "UID: $UID"
echo "HOME: $HOME"
$
```

The $USER, $UID, and $HOME environment variables are used to display the pertinent information about the logged-in user. The output should look something like this:

```bash
$ chmod u+x test2
$ ./test2
User info for userid: rich
UID: 501
HOME: /home/rich
$
```

Notice that the environment variables in the echo commands are replaced by their current values when the script is run. Also notice that we were able to place the $USER system variable within the double quotation marks in the first string, and the shell script was still able to figure out what we meant. This is a drawback of using this method though. Look at what happens in this example:

```bash
$ echo "The cost of the item is $15"
The cost of the item is 5
```

That is obviously not what I intended. Whenever the script sees a dollar sign within quotes, it assumes you're referencing a variable. In this example the script attempted to display the variable $1 (which was not defined), and then the number 5. To display an actual dollar sign, you must precede it with a backslash character:

```bash
$ echo "The cost of the item is \$15"
The cost of the item is $15
```

That's better. The backslash allowed the shell script to interpret the dollar sign as a literal character. You can also use curly braces to clearly define the variable name, which is useful when the variable is followed by other characters:

```bash
$ echo "The cost of the item is ${variable}15"
```
