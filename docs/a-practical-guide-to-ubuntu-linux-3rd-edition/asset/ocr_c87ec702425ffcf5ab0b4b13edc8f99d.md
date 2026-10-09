from a startup file. Typically you want these variables to apply to all subshells you start as well as to your login shell. For those variables not automatically exported by the shell, you must use export (page 992) to make them available to child shells.

# HOME: YOUR HOME DIRECTORY

By default your home directory is the working directory when you log in. Your home directory is established when your account is set up; its name is stored in the /etc/passwd file.

```
$ grep sam /etc/passwd
sam:x:501:501:Sam S .x301::/home/sam:/bin/bash
```

When you log in, the shell inherits the pathname of your home directory and assigns it to the variable HOME. When you give a cd command without an argument, cd makes the directory whose name is stored in HOME the working directory:

```
$ pwd
/home/max/laptop
$ echo $HOME
/home/max
$ cd
$ pwd
/home/max
```

This example shows the value of the HOME variable and the effect of the cd builtin. After you execute cd without an argument, the pathname of the working directory is the same as the value of HOME: your home directory.

Tilde (~) The shell uses the value of HOME to expand pathnames that use the shorthand tilde (~) notation (page 206) to denote a user’s home directory. The following example uses echo to display the value of this shortcut and then uses ls to list the files in Max’s laptop directory, which is a subdirectory of his home directory:

```
$ echo ~
/home/max
$ ls ~/laptop
tester count lineup
```

# PATH: WHERE THE SHELL LOOKS FOR PROGRAMS

When you give the shell an absolute or relative pathname rather than a simple filename as a command, it looks in the specified directory for an executable file with the specified filename. If the file with the pathname you specified does not exist, the shell reports command not found. If the file exists as specified but you do not have execute permission for it, or in the case of a shell script you do not have read and execute permission for it, the shell reports Permission denied.

If you give a simple filename as a command, the shell searches through certain directories (your search path) for the program you want to execute. It looks in several directories for a file that has the same name as the command and that you have execute permission for (a compiled program) or read and execute permission for (a shell script). The PATH shell variable controls this search.