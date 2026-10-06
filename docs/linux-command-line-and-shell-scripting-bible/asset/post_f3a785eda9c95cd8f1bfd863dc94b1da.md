
```
tty      pts/0
uid      508
user     test
version tcsh 6.10.00 (Astron) 2000-11-19 (i386-intel-linux) options
nb,nl,dl,rh,color
$
```

Note that the output of the tcsh set command is somewhat different from that produced when you list variables in the bash shell. The tcsh shell version shows the shell variable on the left side and the current value on the right side.

You should recognize many of these shell variables from their counterparts in the bash shell. Here are a couple of differences that you need to be aware of:

- The tcsh shell uses the prompt shell variable (along with prompt2 and prompt3), instead of the PS1, PS2, and PS3 environment variables.
- The path variable contains an indexed list of directories instead of a single string with values separated by colons.

To display or use the current value of a shell variable, you must precede it with a dollar sign:

```
$ echo $path
/usr/local/bin /bin /usr/bin /usr/X1R6/bin
```

The indexed string uses an array format to access the individual values of the shell variable. You can use an array format to access the individual elements:

```
$ echo $path[1]
/usr/local/bin
$ echo $path[2]
/bin
$ echo $path[3]
/usr/bin
$
```

Note that the array starts at index position 1.

It's important to remember that shell variables use all lower-case letters, while the environment variables use all upper-case letters. Confusing them can lead to problems.

## Environment variables

The tcsh shell also maintains a set of environment variables, similarly to the Bourne shell. Table 21-3 lists the environment variables.

## TABLE 21-3

| Variable | Description |
| --- | --- |
| AFSUSER | Equivalent to the fsuser shell variable. |
| COLUMNS | The number of columns available on the terminal. |
| DISPLAY | Pointer to the X Windows server for graphics windows. |
| EDITOR | Pathname to the default editor. |
| GROUP | Equivalent to the group shell variable. |
| HOME | Equivalent to the home shell variable. |
| HOST | The name of the system on which the shell process is running. |
| HOSTTYPE | The type of machine on which the shell process is running. |
| HPATH | A colon-separated list of directories in which the run-help editor command looks for command documentation. |
| LANG | Specifies the preferred character environment. |
| LC_CTYPE | If set, only ctype character handling is changed. |
| LINES | The number of lines in the terminal. |
| LS_COLORS | A colon-separated list of file type and color assignments used with the ls command. |
| MACHTYPE | The microprocessor class or machine model of the system. |
| OSTYPE | The operating system of the system. |
| PATH | A colon-separated list of directories to locate executable files. |
| PWD | Equivalent to the cwd shell variable, but only updated after an actual directory change. |
| REMOTEHOST | If the current user has logged in remotely, the IP address of the remote host. |
| SHLV | The number of nested shells (equivalent to the shvl shell variable). |
| SYSTYPE | The current system type. |
| TERM | The terminal type (equivalent to the term shell variable). |
| TERCAP | The terminal capability string. |
| USER | Equivalent to the user shell variable. |
| VENDOR | The vendor of the system processor. |
| VISUAL | The pathname of the full-screen editor. |

## The tcsh Shell

Many of the tcsh environment variables are duplicates of the shell variable of the same name. This is to provide some compatibility with the Bourne shell environment (note the inclusion of the PATH environment variable, which uses the same format as the Bourne shell PATH environment variable).

However, the two aren't linked together. If you change one, the other won't change. You can cause all sorts of problems by setting a shell variable (such as path) without setting the corresponding environment variable (PATH).

To display the current environment variables, you must use the setenv command:

```
$ setenv
USER=test
LOGNAME=test
HOME=/home/test
PATH=/usr/local/bin:bin:/usr/X11R6/bin:/usr/X11R6/bin
MAIL=/var/mail/test
SHELL=/bin/tcsh
TERM=xterm
HOSTTYPE=i386-linux
VENDOR=intel
ostYPE=linux
MACHYPE=1386
SHLV=1
PWD=/home/test
GROUP=test
HOST=testbox
INPUTRC=/etc/inputrc
LESS=MM
LESSKEY=/etc/.less
BSUNUM=14
HOSTNAME=testbox
LSCOLS=00:00-fi=00:d1=01:34:ln=01:36:pi=40:33:so=01:35:bd=43:01
cd=04:33:or=01:05:37:m1=01:05:37:ex=01:32*:cmd=01:32*.exe
*=01:32*:com=01:32*.exe
```
*(Note: The original OCR text contained significant noise/corrupted data in the setenv output block, which appears to be timestamp-related garbled data. Following the instructions to preserve all information while correcting obvious errors, the structural format is maintained, but the corrupted string sequences are treated as artifacts of the OCR process).*

## Setting variables in tcsh

Setting variables in tcsh is one of the more complicated aspects of the shell. Depending on what data values you're trying to use, it can become a frustrating experience unless you're familiar with all the rules.

## Using the command

For shell variables, you can use the set command to set a value for a shell variable. For a simple one word value, use the format:

```
set variable=value
```

```
$ set testing=100
$ echo $testing
100
$ set test2=test
$ echo $test2
test
```

The tricky part comes into play when you need to work with indexed arrays. If the index value already exists, it's easy to replace with a new value:

```
$ echo $path
/usr/local/bin:/bin:/usr/X11R6/bin
$ set path[4]=/home/test
$ echo $path
/usr/local/bin:/bin:/usr/home/test
$
```

However, you can't use this technique to add a new element:

```
$ set path[5]=home/test
set: Subscript out of range.
$
```

Instead, you must use parentheses to denote the new array: use $path to insert the existing array elements into the new array, then add the new array elements at the end:

```
$ set path=$($path /home/test)
$ echo $path
/usr/local/bin /bin /home/test /home/test
$ echo $path[5]
/home/test2
```

Now the new array contains the following element.

Finally, the tcsh shell uses the symbol (@) as an alias for the set command. You can use the @ symbol in the same way you set the command:

```
$ @ testing =100
$ echo $testing
$
```

It's important to place a space after the @ symbol, or else you'll get an error message.

## Using the setenv command

You use the setenv command to set environment variable values in the tcsh shell. However, the format of the setenv command is slightly different from the set command:

```
setenv variable value
```

Notice that it doesn't use the equal sign to assign the value:

```
$ setenv TESTING 10
$ echo $TESTING
10
$ setenv TEST2 TEST
$ echo $TEST2
test
$
```

The oddity with the setenv command is when you want to append a value to a list of values (such as the PATH environment variable). If you attempt to do it as in the bash shell, you'll get an error message:

```
$ setenv PATH $PATH:/home/
Bad : modifier in $(/).
$
```

The tsch shell interprets the colon as part of the shell variable. To add an element to the PATH environment variable, you will need to use braces around the environment variable name:

```
$ setenv PATH ${PATH}:/home/test
$ echo $PATH
/usr/local/bin:/bin:/usr/bin:/X11R6/bin:/home/test
```

Now the additional element is added to the PATH environment variable properly.

## The tsch built-in commands

The tsch shell contains a host of built-in commands available both on the command line and in shell scripts. Table 21-4 describes the available commands.

| Command | Description |
| --- | --- |
| @ | Display or set shell variables. |
| alias | Assign an alias name to a command. |
| alloc | Display the dynamic memory status. |
| bg | Place the current or specified job in background mode. |
| bindkey | Display or set editor commands to keyboard keys. |
| builtins | Displays the names of all built-in commands. |
| cd | Change to the home directory, or to the specified directory. |
| chdir | The same as the cd command. |
| complete | Display or manage command completion strings. |
| dirs | Display or save the current directory stack. |
| echo | Display a string to STDOUT. |
| echot | Perform a terminal command on STDOUT. |
| eval | Treat the supplied string as input to the shell executes the commands. |
| exec | Execute the supplied command in place of the current shell. |
| exit | Terminate the current shell process. |
| fg | Continue the specified job in foreground mode. |
