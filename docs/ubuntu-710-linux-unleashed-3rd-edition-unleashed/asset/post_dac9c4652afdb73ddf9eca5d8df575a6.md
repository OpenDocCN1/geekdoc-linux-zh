
practice for all shell scripting. For example, if you write a shell script using bash, but want the script to execute as if run by the Bourne shell, sh, the first line of your script will contain #!/bin/sh, which is a link to the bash shell. Running bash as sh will cause bash to act as a Bourne shell. This is the reason for the symbolic link sh, which points to bash.

## The Shebang Line

The shebang line is a magic number, as defined in /usr/share/magic—a text database of magic numbers for the Linux file command. Magic numbers are used by many different Linux commands to quickly identify a type of file, and the database format is documented in the section five manual page named magic (read by using man 5 magic). For example, magic numbers can be used by the Linux file command to display the identity of a script (no matter what filename is used) as a shell script using a specific shell or other interpreter such as awk or Perl.

You might also find different or new environment variables available to your scripts by using different shells. For example, if you launch csh from the bash command line, you will find several new variables or variables with slightly different definitions, such as

```
$ env
...
VENDOR=intel
MACHTYPE=i386
HOSTTYPE=i386-linux
HOST=thinkpad.home.org
```

On the other hand, bash might provide these variables or variables of the same name with a slightly different definition, such as

```
$ env
...
HOSTTYPE=i386
HOSTNAME=thinkpad.home.org
```

Although the behavior of a shebang line is not defined by POSIX, variations of its use can be helpful when you are writing shell scripts. For example, as described in the wish man page, you can use a shell to help execute programs called within a shell script without needing to hard code pathnames of programs. The wish command is a windowing Tool Control Language (tcl) interpreter that can be used to write graphical clients. Avoiding the use of specific pathnames to programs increases shell script portability because not every Unix or Linux system has programs in the same location.

For example, if you want to use the wish command, your first inclination might be to write

```
#!/usr/local/bin/wish
```

Although this will work on many other operating systems, the script will fail under Linux because wish is located under the /usr/bin/ directory. However, if you write the command line this way:

```
#!/bin/sh
exec wish "$@"
```

You can use the wish command (as a binary or a shell script itself); your first inclination might be to write in Linux.

## Using Variables in Shell Scripts

When writing shell scripts for Linux, you work with three types of variables:

- **Environment Variables**—Part of the system environment, you can use them in your shell program. New variables can be defined, and some of them, such as `PATH`, can also be modified within a shell program.
- **Built-in variables**—These are variables such as options used on the command (interpreted by the shell as a *positional argument*) are provided by Linux. Unlike environment variables, you cannot modify them.
- **User variables**—Defined by you when you write a shell script. You can use and modify them at will within the shell program.

A major difference between shell programming and other programming languages is that in shell programming, variables are not *typed*—that is, you do not have to specify whether a variable is a number or a string, and so on.

## Assigning a Value to a Variable

Say that you want to use a variable called lcount to count the number of iterations in a loop within a shell program. You can declare and initialize this variable as follows:

| Command | Environment |
|---|---|
| `lcount=0` | `pdksh` and `bash` |
| `set lcount=0` | `tcsh` |

> **NOTE**
> 
> Under pdksh and bash, you must ensure that the equal sign (=) does not have spaces before and after it.

To store a string in a variable, you can use the following:

| Command | Environment |
|---|---|
| myname=Sanjiv | pdksh and bash |
| set myname=Sanjiv | tcsh |

Use the preceding variable form if the string doesn't have embedded spaces. If a string has embedded spaces, you can do the assignment as follows:

| Command | Environment |
|---|---|
| myname="Sanjiv Guha" | pdksh and bash |
| set myname="Sanjiv Guha" | tcsh |

## Accessing Variable Values

You can access the value of a variable by prefixing the variable name with a $ (dollar sign). That is, if the variable name is var, you can access the variable by using $var.

If you want to assign the value of var to the variable lcount, you can do so as follows:

| Command | Environment |
|---|---|
| lcount=$var | pdksh and bash |
| set lcount=$var | tcsh |

## Positional Parameters

It is possible to pass options from the command line or from another shell script to your shell program.

These options are supplied to the shell program by Linux as positional parameters, which have special names provided by the system. The first parameter is stored in a variable called 1 (number 1) and can be accessed by using $1 within the program. The second parameter is stored in a variable called 2 and can be accessed by using $2 within the program, and so on. One or more of the higher numbered positional parameters can be omitted while you're invoking a shell program.

Understanding how to use these positional parameters and how to access and use variables retrieved from the command line is necessary when developing more advanced shell programs.

## A Simple Example of a Positional Parameter

For example, if a shell program myprog expects two parameters—such as a first name and a last name—you can invoke the shell program with only one parameter, the first name. However, you cannot invoke it with only the second parameter, the last name.
