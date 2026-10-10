```
export PATH
# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
$ 
```

The .bashrc file does two things. First, it checks for a common bashrc file in the /etc directory. Second, it provides a place for the user to enter personal command aliases (discussed in Chapter 5) and script functions (described in Chapter 17).

# Understanding the noninteractive shell process

The last type of shell is a *noninteractive subshell*. This is the shell where the system can start to execute a shell script. This is different in that there isn't a CLI prompt to worry about. However, you may want to run specific startup commands each time you start a script on your system.

![](bbox=[0.11, 0.48, 0.9, 0.64])

To accommodate that situation, the Bash shell provides the BASH_ENV environment variable. When the shell starts a noninteractive subshell process, it checks this environment variable for the startup file name to execute. If one is present, the shell executes the file's commands, which typically include variables set for the shell scripts.

On this CentOS Linux distribution, this environment value is not set by default. When a variable is not set, the printenv command simply returns the CLI prompt:

```
$ printenv BASH_ENV
$ 
```