
Variables allow you to set aside locations in memory to temporarily store information and then recall that information later in the script by referencing the variable name.

There are two types of variables available in the Linux shell. The following sections explain how to use both types in your shell scripts.

## Environment Variables

*Environment variables* track specific system information, such as the name of the system, the name of the user logged into the shell, the user's user ID (UID), the default home directory for the user, and the search path the shell uses to find executable programs. You can display a complete list of active environment variables available in your shell by using the `set` command, as shown in Listing 25.6.

**Listing 25.6: Using the set command**
```bash
$ set
BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extglob:extquote
:force_fignore:histappend:interactive_comments:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=()
BASH_ARGV=()
BASH_CMDS=()
BASH_COMPLETION_VERSINFO=([0]="2" [1]="8")
BASH_LINENO=()
BASH_SOURCE=()
BASH_VERSION=[0]="4" [1]="4" [2]="19" [3]="1" [4]="release" [5]="x86_64-pc-linux-gnu")
BASH_VERSION='4.4.19(1)-release'
CLUTTER_IM_MODULE=xim
COLORTERM=truecolor
COLUMNS=80
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
DESKTOP_SESSION=ubuntu
DIRSTACK=()
DISPLAY=::0
EUID=1000
GDMSESSION=ubuntu
...
```

There are environment variables that track just about every feature of the command-line shell. You can tap into these environment variables from within your scripts by using the environment variable name preceded by a dollar sign, as shown in Listing 25.7.

**Listing 25.7:** The *test2.sh* shell script file to display environment variables

```bash
$ cat test2.sh
#!/bin/bash
# display user information from the system.
echo User info for userid: $USER
echo UID: $UID
echo HOME: $HOME
$ 
```

The $USER, $UID, and $HOME environment variables are commonly used to display information about the logged-in user. If you run the *test2.sh* shell script shown in Listing 25.7, the output should look like this:

```bash
$ chmod u+x test2.sh
$ ./test2.sh
User info for userid: rich
UID: 1000
HOME: /home/rich
$ 
```

The values you see should be related to your user account. This allows you to dynamically retrieve information about the user account running your shell script to customize the output.

> **TIP**
> If you write shell scripts to distribute for other Linux administrators to use, two additional helpful environment variables are the `$SHELL` variable, which returns the current shell program the script is running in, and the `$PATH` variable, which returns a list of directories the shell will look in to find commands. It's usually a good idea to check these two environment variables to make sure your script will run correctly in any Linux environment.

### User Variables

*User variables* allow you to store your own data within your shell scripts. You assign values to user variables using the equal sign. Spaces must not appear between the variable name, the equal sign, and the value. Here are a few examples:

```bash
var1=10
var2=23.45
var3=testing
var4="Still more testing"
```

The shell script automatically determines the data type used for the variable value. Variables defined within the shell script are called *local variables* and are accessible only from within the shell script. *Global variables* are defined outside the shell script at the main shell level and are inherited by the script shell environment.

![](img/c0a399aca0d18f8822d714ad0a173123_774_0.png)

> The `set` command displays all of the global variables set. If you need to see the local variables set for your session, use the `printenv` command. The `export` command allows you to mark a variable as exportable, which means any child processes spawned from your shell will see it. Finally, the `env` command allows you to run a script and modify environment variables internal to the script without affecting the system environment variables.

Just as with environment variables, you can reference user variables using the dollar sign. Listing 25.8 shows an example of writing a shell script that uses user variables.

**Listing 25.8:** Using user variables in a shell script

```bash
$ cat test3.sh
#!/bin/bash
# testing variables
days=10
guest=Katie

echo $guest checked in $days days ago
$
```

Running the test3.sh script from Listing 25.8 produces the following output:

```bash
$ chmod u+x test3.sh
$ ./test3.sh
Katie checked in 10 days ago
$
```

After you store the data in a user variable, you can reference it anywhere in your shell script!

## Command-Line Arguments

One of the most versatile features of shell scripts is the ability to pass data into the script when you run it. This allows you to customize the script with new data each time you run it.

One method of passing data into a shell script is to use *command-line arguments*. Command-line arguments are data you include on the command line when you run the command. Just start listing them after the command, separating each data value with a space, in this format:

```text
command argument1 argument2 ...
```

You retrieve the values in your shell script code using special numeric *positional variables*. Use the variable `$1` to retrieve the first command-line argument, `$2` the second argument, and so on. Listing 25.9 shows how to use positional variables in your shell script.

**Listing 25.9: Using command-line arguments in a shell script**

```bash
$ cat test4.sh
#!/bin/bash
# Testing command line arguments
echo $1 checked in $2 days ago
$ chmod u+x test4.sh
$ ./test4.sh Barbara 4
Barbara checked in 4 days ago
$ ./test4.sh Jessica 5
Jessica checked in 5 days ago
$
```

The test4.sh shell script uses two command-line arguments. The `$1` variable holds the name of the person, and the `$2` variable holds the number of days ago they checked in. When you run the test4.sh shell script, be sure to include both data values in the command line. The shell won’t produce an error message if a positional variable doesn’t exist; you just won’t get the results you expected:

```bash
$ ./test4.sh rich
rich checked in days ago
$
```

It’s up to you to check if the positional variable exists within your program code. We’ll explore how to do that later when we discuss logic statements.

## The Exit Status

When a shell script ends, it returns an exit status to the parent shell that launched it. The exit status tells us whether or not the shell script completed successfully.

Linux provides us with the special `$?` variable, which holds the exit status value from the last command that executed. To check the exit status of a command, you must view the `$?` variable immediately after the command ends. It changes values according to the exit status of the last command executed by the shell:

```bash
$ who
rich :0    2019-02-20 23:16 (:0)
$ echo $?
0
$
```

By convention, the exit status of a command that successfully completes is 0. If a command completes with an error, then a positive integer value appears as the exit status.

You can change the exit status of your shell scripts by using the `exit` command. Just specify the exit status value you want in the `exit` command:

```bash
$ /bin/bash
$ exit 120
exit
$ echo $?
120
$
```

In this example we started a new child shell with the `/bin/bash` command and then used the `exit` command to exit the child shell with an exit status code of 120. Back in the parent shell, we then displayed the `$?` variable value to see if it matched what we had set in the `exit` command. As you write more complicated scripts, you can indicate errors by changing the exit status value. That way, by checking the exit status, you can easily debug your shell scripts.

## Writing Script Programs

So far we’ve explored how to combine regular command-line commands within a shell script to automate common tasks that you may perform as the system administrator. But shell scripts allow us to do much more than just that. The Bash shell provides more programming-like commands that allow us to write full-fledged programs within our shell scripts, such as capturing command output, performing mathematical operations, checking variable and file conditions, and looping through commands. The following sections walk you through some of the advanced programming features available to you from the Bash shell.

### Command Substitution

Quite possibly one of the most useful features of shell scripts is the ability to store and process data. So far we’ve discussed how to use output redirection to store output from a command to a file and piping to redirect the output of a command to another command. There’s another technique, however, that can give you more flexibility in storing and using data in your scripts.

*Command substitution* allows you to assign the output of a command to a user variable in the shell script. After the output is stored in a variable, you can use standard Linux string manipulation commands (such as `sort` or `grep`) to manipulate the data before displaying it.

To redirect the output of a command to a variable, you need to use one of two command substitution formats:

- Placing backticks (`\``) around the command
- Using the command within the `$()` function
