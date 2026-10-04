# 432 Exploring the User Environment

(By the way, the right of bin/env command also displays the environment, but env is shorter.)

The env command prints a long list of lines. That collection of lines is the current environment, and each line defines an environment variable. For example, the env command displays this typical line:

```
HOSTNAME=localhost.localdomain
```

This line defines the environment variable HOSTNAME, and it's defined as localhost.localdomain.

An environment variable is nothing more than a name associated with a string. For example, the environment variable PATH is typically defined as:

```
PATH=/usr/local/bin:/usr/bin:/usr/X11R/bin
```

The string to the right of the equal is the value of the PATH environment variable. By convention, the PATH environment variable is a sequence of directories, each name separated from the preceding one by a colon (:).

Each environment variable has a specific purpose. When the shell has to search for a file, it searches the directories listed in the PATH environment variable. The shell searches the directories in PATH in the order of their appearance. Therefore, if two programs have the same name, the shell executes the one it finds.

In a fashion similar to the shell's use of the PATH environment variable, an editor as vi uses the value of the TERM environment variable to figure out how to display the file you are editing with vi. To see the current setting of TERM, type the following command at the shell prompt:

```
echo $TERM
```

If you type this command in a terminal window, the output is as follows:

xterm

To define an environment variable in Bash, use the following syntax:

```
export NAME=Value
```

Here, NAME denotes the name of the environment variable, and Value is the string representing its value. Therefore, you set TERM to the value xterm by using the following command:

```
export TERM=xterm
```