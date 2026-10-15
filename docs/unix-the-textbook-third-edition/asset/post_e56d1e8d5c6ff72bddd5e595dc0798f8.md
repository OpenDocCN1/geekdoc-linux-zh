
```
SSH_CONNECTION='202.147.168.98 50256 202.147.169.196 22'
SSH_TTY=/dev/pts/1
TERM=xterm-color
USER=sarwar
VENDOR=amd
_=MAC
no_proxy=127.0.0.1,localhost
$
```

You can also use the env (System V) and printenv (BSD) commands to display the names of the environment variables and their values, but the list is not as complete as the one displayed by the set command. In particular, the output does not include any user-defined variables. The following is a sample output of the env command on the same system that we ran the set command on.

```
$ env
VENDOR=amd
SSH_CLIENT=202.147.168.98 50256 22
LOGNAME=sarwar
PAGER=more
LANG=en_US.UTF-8
no_proxy=127.0.0.1,localhost
OSTYPE=FreeBSD
NO_PROXY=127.0.0.1,localhost
MACH_TYPE=x86_64
CLICOLOR=true
MAIL=/var/mail/sarwar
PATH=/usr/local/share/pcbsd/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/games:/usr/pbi/bin:/usr/local/sbin:/usr/local/bin:/home/sarwar/bin
EDITOR=vi
HOST=pcbsd-srv
REMOTEHOST=static-host202-147-168-98.link.net.pk
PWD=/home/sarwar
GROUP=sarwar
TERM=xterm-color
SSH_TTY=/dev/pts/1
HOME=/home/sarwar
USER=sarwar
SSH_CONNECTION=202.147.168.98 50256 202.147.169.196 22
HOSTTYPE=FreeBSD
SHELL=/bin/csh
MORE=-erX
MANPATH=/usr/share/man:/usr/local/man:/usr/share/openssl/man:/usr/pbi/man:/usr/local/lib/perl5/5.16/man:/usr/local/lib/perl5/5.16/perl/man
```

```
BLOCKSIZE=K
SHLVL=1
$
```

In the following in-chapter exercises, you will create a simple shell script and make it executable. Also, you will use the set, printenv, and env commands to display the names and values of the shell variables on your system.

## EXERCISE 12.1

Display the names and values of all the shell variables on your UNIX machine. What command(s) did you use?

## EXERCISE 12.2

Create a file that contains a shell script comprising the date and pwd commands, one on each line. Make the file executable and run the shell script. List all the steps for completing this task.

### 12.3.1 Reading and Writing Shell Variables

The syntax for the assignment statement in the Bourne shell is as follows. The command syntax variable=value comprises what is commonly known as the assignment statement, and its purpose is to assign a value to a variable. The evaluation of the assignment statement is right to left. Thus, value is evaluated first and then assigned to variable. If there is a problem in evaluating value, an error is reported.

## SYNTAX

```
variable1=value1 [variable2=value2 ... variableN=valueN]
```

Purpose: Assign values value1, ..., valueN to variables variable1, ..., variableN, respectively; no space allowed before or after the equal sign

Note that there is no space before and after the equals sign (=) in the syntax. If a value contains spaces, you must enclose the value in quotes. Single and double quotes work differently, as discussed later in this section. You can refer to (i.e., access) the current value of a variable by placing a dollar sign ($) before the variable name; there is no space between $ and the variable name. You can use the echo command to display the values of shell variables.

Single quotes should be used to preserve the literal meanings of all characters, except single quotes. Double quotes preserve the literal meaning of all characters except single quotes, dollar signs, and backslashes. A backslash preserves the literal meaning of the character that follows, except \n. The newline character (\n) has special meaning, and in order to preserve this meaning, it must be enclosed in single quotes, as in '\n'. A backslash in double quotes remains literal, unless it precedes the following characters: backlash,

single quote, double quotes, dollar sign, and newline. Enclosing characters between $' and ' preserves the literal meaning of all characters, except single quotes and backslashes. \t and \b also have special meaning and stand for tab and backspace, respectively.

The following session shows a few examples of quoting, $$ stands for the PID of the process that executes the echo command—that is, the current shell process. You can prove it by running the ps command and verifying that 61358 is, in fact, the PID of your current Bourne shell process.

```
$ echo '$name * ? \'
$name * ? \
$ echo "$ $ * \n ?"
$ * \n ?
$ echo "$$ * \n ?"
61358 * \n ?
$ echo "\$\' \" \\ \\\n"
$ \' " \\ n
$ echo $'a d ? * " $'
a d ? * " $
$ echo $'a \ ? * " $'
Syntax error: Bad escape sequence
$ echo $'a ' ? * " $'
>
```

The following session shows how shell variables can be created and read, and how their values may be changed.

```
$ name=John
$ echo $name
John
$ name=John Doe
Doe: not found
$ name=John date
Sun Aug 3 09:44:35 PKT 2014
$ echo $name
$ name="John Doe"
$ echo $name
John Doe
$ name=John*
$ echo $name
John.Bates.letter John.Johnsen.memo John.email1
$ echo "$name"
John*
$ echo "The name $name sounds familiar!"
The name John* sounds familiar!
$ echo \$name
$name
```
