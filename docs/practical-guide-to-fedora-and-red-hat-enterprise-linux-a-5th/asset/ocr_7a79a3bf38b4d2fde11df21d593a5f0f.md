```
declare -r SHELLOPTS="braceexpand:emacs:hashall:hstexpnad:history:..."
declare -ir UID="500"
declare -r person2="jenny"
declare -rx person3="helen"
```

The first five entries are keyword variables that are automatically declared as read-only. Some of these variables are stored as integers (-i). The -a option indicates that BASH_VERSINFO is an array variable; the value of each element of the array is listed to the right of an equal sign.

By default the values of variables are stored as strings. When you perform arithmetic on a string variable, the shell converts the variable into a number, manipulates it, and then converts it back to a string. A variable with the integer attribute is stored as an integer. Assign the integer attribute as follows:

```
$ typeest -i COUNT
```

# KEYWORD VARIABLES

Keyword variables either are inherited or are declared and initialized by the shell when it starts. You can assign values to these variables from the command line or from a startup file. Typically you want these variables to apply to all subshells you start as well as to your login shell. For those variables not automatically exported by the shell, you must use export (page 926) to make them available to child shells.

# HOME: YOUR HOME DIRECTORY

By default your home directory is your working directory when you log in. Your home directory is determined when you establish your account; its name is stored in the /etc/passwd file.

```
$ grep sam /etc/passwd
sam:x:501:501:Sam S. x301:/home/sam:/bin/bash
```

When you log in, the shell inherits the pathname of your home directory and assigns it to the variable HOME. When you give a cd command without an argument, cd makes the directory whose name is stored in HOME the working directory:

```
$ pwd
/home/alex/laptop
$ echo $HOME
/home/alex
$ cd
$ pwd
/home/alex
```

This example shows the value of the HOME variable and the effect of the cd builtin. After you execute cd without an argument, the pathname of the working directory is the same as the value of HOME: your home directory.

Tilde (--) The shell uses the value of HOME to expand pathnames that use the shorthand tilde (--) notation (page 193) to denote a user's home directory. The following example