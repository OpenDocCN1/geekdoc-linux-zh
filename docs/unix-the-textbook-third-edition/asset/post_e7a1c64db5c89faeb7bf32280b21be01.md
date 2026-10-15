
```
$ echo '$name'
$name
$
```

If the right-hand side of an assignment statement is not enclosed in quotes and includes spaces, the shell assumes that the second and remaining words in the right-hand side form a command, and tries to execute them. The shell displays an error message if the assumed command does not correspond to a valid command, as shown in the statements name=John Doe and name=John date in the previous session. Also, after the name=John* statement has been executed and $name is not quoted in the echo command, the shell lists the file names in your present working directory that match John*, with * considered as the shell metacharacter. In this case, the variable $name must be enclosed in quotes to refer to John*, as in echo "$name". However, if your current directory does not contain any file that starts with the string John, the echo John* command displays John*.

A command consisting of $variable only results in the value of variable executed as a shell command. If the value of variable comprises a valid command, the expected results are produced. If variable does not contain a valid command, the shell, as expected, displays an appropriate error message. The following session makes this point with some examples. The variable used in the session is command.

```
$ command=pwd
$ $command
/home/sarwar/unixb3e/examples
$ command=hello
$ $command
hello: not found
$
```

## 12.3.2 Command Substitution

Command substitution allows you to replace a command with its output. The following is a brief description of command substitution. Note the use of back quotes (also known as grave accents) in the first form of the syntax. In our example shell sessions and scripts throughout the book, we will use the first syntax.

```
SYNTAX
`command`

Or

$(command)

Purpose: Execute command and substitute `command` or $(command), if you use this syntax) with the output of the command
```

The following session illustrates this concept with a few examples. In the first assignment statement, the variable command is assigned a value pwd. In the second and third assignment statements, the output of the pwd command is assigned to the command variable.

```
$ command=pwd
$ echo "The value of command is: $command."
The value of command is: pwd.
$ command=`pwd`
$ echo "The value of command is: $command."
The value of command is: /home/sarwar/unix3e.
$ command=$(pwd)
$ echo "The value of command is: $command."
The value of command is: /home/sarwar/unix3e.
$
```

Command substitution can be specified in any command. For example, in the following session, the output of the date command is substituted for `date` before the echo command is executed.

```
$ echo "The date and time are `date` ."
The date and time are Thu Jul 24 23:59:11 PKT 2014.
$
```

We demonstrate the real-world use of command substitution in various ways throughout this chapter and Chapter 13.

The following in-chapter exercises are designed to reinforce the creation and use of shell variables and the concept of command substitution.

### EXERCISE 12.3

Assign your full name to a shell variable called myname and echo its value. How did you accomplish the task? Show your work.

### EXERCISE 12.4

Assign the output of the echo "Hello, world!" command to the myname variable and then display the value of myname. List the commands that you executed to complete your work.

## 12.3.3 Exporting Environment

When a variable is created in a shell, subsequent shells do not have automatic access to it. The export command passes the value of a variable to subsequent shells. Thus, when a shell script is called and executed in another shell script, it does not get automatic access to the variables defined in the original (i.e., caller) script unless they are explicitly made available to it. The export command can be used to pass the value of one or more shell variables to any subsequent script. All read/write shell environment variables are available to every command, script, and subshell, so they are exported at the time they are initialized. The following is a brief description of the export command.

### SYNTAX

```
export [name-list]
```

**Purpose:** Export the names and copies of the current values in name-list to every command executed from this point on

The following session presents a simple use of the export command. The name variable is initialized to John Doe and is exported to subsequent commands executed under the current shell and any subshells that run under the current shell.

```
$ name="John Doe"
$ export name
$
```

We now illustrate the concept of exporting shell variables via some simple shell scripts. Consider the following session. Note that the one-line shell script in the display_name file displays a null string even though we initialized the name variable to John Doe just before executing this script. The reason is that the name variable is not exported before running the script, and the name variable used in the script is local to the script. Because this local variable name is uninitialized, the echo command displays the null string—the default value of every uninitialized variable.

```
$ cat display_name
echo $name
exit 0
$ name="John Doe"
$ ./display_name
$
```

You can use the exit command to transfer control to the calling process—the current shell process in the preceding session. The only argument of the exit command is an optional integer number, which is returned to the calling process as the exit status of the terminating process. All UNIX commands return an exit status of zero upon success (i.e., if they successfully perform their tasks and terminate normally) and nonzero upon failure. The return status value of a command is stored in the read-only environment variable $?, which can be checked and/or displayed by the calling process. In shell scripts, the status of a command is commonly checked and subsequent action taken. We show the use of $? in
