to all shells and other programs you fork from the original shell. One naming convention is to use only uppercase letters for global variables and to use mixed-case or lowercase letters for other variables. Refer to “Locality of Variables” on page 992 for more information on global variables.

To assign a value to a variable in the Bourne Again Shell, use the following syntax:

```
VARIABLE=value
```

There can be no whitespace on either side of the equal sign (=). An example assignment follows:

```
$ myvar=abc
```

The Bourne Again Shell permits you to put variable assignments on a command line. This type of assignment creates a variable that is local to the command shell—that is, the variable is accessible only from the program command runs. The my_script script displays the value of TEMPDIR. The command runs my_script with TEMPDIR the shell has no value for TEMPDIR after running my_script. If TEMPDIR had been set in the interactive shell, running my_script in this manner would have no effect on its value.

```
$ cat my_script
echo $TEMPDIR
$TEMPDIR=/home/sam/temp .my_script
/home/sam/temp
$echo $TEMPDIR
```

```
$
```

Keyword shell variables (or simply keyword variables) have special meaning to the shell and usually have short, mnemonic names. When you start a shell (by logging in, for example), the shell inherits several keyword variables from the environment. Among these variables are HOME, which identifies your home directory, and PATH, which determines directories the shell searches and in what order to locate commands that you give the. The shell creates and initializes (with default values) other keyword variables when you start it. Still other variables do not exist until you start them.

You can change the values of most keyword shell variables. It is usually necessary to change the values of keyword variables initialized in the /etc/profile or /etc/csh.csh system files. If you need to change the value of a bash keyword variable, do so in one of your startup files (page 293). Just as you can make user-created variables global, so you can make keyword variables global—a task usually automatically in startup files. You can also make a keyword variable readonly.

Positional and special parameters The names of positional and special parameters do not resemble variable names. Most of these parameters have one-character names (for example, 1, ?, and #)