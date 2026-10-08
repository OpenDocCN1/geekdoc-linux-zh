An **alias** is a name that represents another command. You can use aliases to simplify and automate commands you use frequently. For example, the following command sets up an alias for the rm command.

```
alias rm="rm -i"
```

This command above causes the rm -i command to execute any time the user enters the rm command. This is a commonly used alias, as it ensures users are always prompted before the rm command deletes a file. Here are two other common aliases that help safeguard files:

```
alias mv="mv -i"
alias cp="cp -i"
```

![](bbox=[0.22, 0.31, 0.98, 0.42])

The **.bashrc** file that resides in your home directory can be used to establish customizations that take effect for each login session. The .bashrc script is executed each time you generate a shell, such as when you run a shell script. Any time a subshell is created, the .bashrc is re-executed. The following .bashrc file is commented to explain how you can make your own changes.

```
.bashrc
# Source global definitions
if [ -f /etc/bashrc ]; then
. /etc/bashrc # if any global definitions are defined
# run them first
alias rm 'rm -i' # make sure user is prompted before
# removing files
alias mv 'mv -i' # make sure user is prompted before
# overwriting files
set -o ignoreeof # Do not allow Ctrl-D to logout
set -o noclobber # Force user to enter >! To write
# over existing files
PS1="\\w \\$" # Set prompt to show working directory
```

In addition to knowing how to customize your work environment, you should also be familiar with the trap command.