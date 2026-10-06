# Keyword Variables (Continued)

# table 15-5

The shell stores the absolute pathname of the working directory, as set by the most recent cd command, in PWD, and the pathname of the previous working directory in OLDPWD. You can toggle be-directories by giving the command cd $OLDPWD.

The value of PWD is not necessarily the same as the value returned by the /bin/pwd command, because the PWD variable keeps track of where you are, but also how you got there.

OLDPWD

```
zsh % cd
zsh % mkdir -p top/level2/level3
zsh % ln -s top/level2 symdir
zsh % cd symdir
zsh % /bin/pwd
/home/alex/top/level2
zsh % echo $PWD
/home/alex/symdir
zsh % pwd
/home/alex/symdir
```

The -option to mkdir causes the command to create any missing intermediate directories (in this case top and level2) when creating the target directory. The Z Shell pwd builtin keeps track of symbolic links; the TC and Bounce Again Shell pwd builds not (page 128). The pwd utility (/bin/pwd) simply tells you the name of the directory you are in, regardless of how you got there.

OPTARG and OPTIND

These variables are set by the getopts builtin. Refer to "Builtings" on page 767.

PATH

The list of directories that the shell searches for commands (page 577).

PPID

The value of the PID of the parent process (the process running that process is evaluating this variable). This value does not change throughout the lifetime of a shell session.

PS1

The shell prompt string (page 579).

PS2

The secondary prompt string (page 579).