# Running Scripts

To execute a Z Shell script, use the script name as an argument to zsh:

```
zsh % zsh script_name
```

The preceding command calls zsh regardless of which shell you are working with. If you have executed permission for the file that contains the script, you can use the filename as a command:

```
zsh % script_name
```

When you start the first line of the script with #!/bin/zsh, the Z Shell runs the script, regardless of what shell you call the script from (page 564):

# Startup Files

The Z Shell uses many of the same environment variables as bash and adds a few others. You can set these variables, along with commands that establish other characteristics of the Z Shell environment, in one of the Z Shell startup files (Table 15-1). All startup files with names that begin with a period reside in your home directory.

| Startup Files | table 15-1 |
| /etc/zhenv | This file is created by Superuser systemwide default characteristics for zsh. It is the first and only file that zsh always reads when it starts. |
| ~/zhenv | You create this file in your home directory. The preferred location to set variables that override those set in /etc/zhenv, is the second file to be read. |
|etc/zprofile | This file is created by Superuser to establish systemwide default characteristics for zsh login shells. It is read when a login shell starts up (or when zsh is called with the -l option) but not when you use the -f option. It is the preferred file for setting systemwide characteristics for users desiring a bash- or ksh-like shell. |
| ~/zprofile | You create this file in your home directory. This file is the preferred location to set variables that override those set in /etc/zprofile and read when a login shell starts up (or when zsh is called with the -l option) but not when the -f option is used. This file is preferred for setting personal characteristics for a bash- or ksh-like shell. |