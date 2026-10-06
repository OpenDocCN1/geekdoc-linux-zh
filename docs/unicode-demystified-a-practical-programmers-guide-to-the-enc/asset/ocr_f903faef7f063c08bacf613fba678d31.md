# Order of Execution of bash Startup Files

| File | Interactive (Login) Shell | Noninteractive (Nonlogin) Shell |
|---|---|--|
| /etc/profile | First | Not executed, but the shell inherits from the parent shell variables that were originally set by these files. |
| .bash_profile | Second | |
| .bash_login | Second if no .bash_profile | |
| .profile | Second if no .bash_profile or .bash_login | |
| .bashrc | Executed only by interactive, nonlocal shells | Not executed. |
| BASH_ENV or ENV | Not executed | Execute the commands listed in the file named by one of these variables. When the shell is started in POSIX mode, the file named by ENV is executed using source. Otherwise, the file named by BASH_ENV is executed. |
| .bash_logout | Executed on logout | Not executed.

Although the numbers of shell types and initialization files might seem confusing, many bash users have only .bash_profile and .bashrc in their home directories. Most of the commands that they want all instances of bash to execute are placed into .bashrc, whereas .bash_profile includes a command to load and run commands from .bashrc, as well as an assignment of the string ~/ to the ENV variable. This way, bashrc is executed, no matter the shell gets started. You can put the following commands into .bash_profile to get this effect:

```
export ENV=~/ bashrc
if [ -f ~/.bashrc ]; then source ~/.bashrc; fi
```

# Parameters and Variables

Within the shell, a shell parameter is associated with a value that is accessible to the user. There are several kinds of shell parameters. Parameters whose name consist