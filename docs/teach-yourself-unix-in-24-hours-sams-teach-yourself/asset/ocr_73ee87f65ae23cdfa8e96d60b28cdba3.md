# Hour 14

```
alias rd      *readmsg $ | page*
alias rn      */usr/local/bin/rm -d$HOME -L -M -m -e -S -ias ssinfo echo "connecting..." login oasis
```

# and some special stuff if we're in an interactive shell

```
if ($?)prompt ) then
# shell is interactive.
alias cd      'cd - |' setprompt'
alias setprompt 'setprompt="$system (cwd) \! : ""*'
```

```
set noclobber history=100systemmentor filec
umask 007
setprompt
if
```

Again, any line that begins with a # is considered a comment. There are, therefore, two primary types of commands in this script: the C shell environment (set) and the command alias (alias). The first defines the PATH I want to use, although in a format slightly different from the colon-separated list by env. The csh command always ensures that the environment variable and variable match, and, although I opt to change the path as a set, I could as easily use setenv PATH.

You all learn aliases in the next hour, but for now you know that the format is alias word (or commands) to execute. When I enter is, for example, you can see the shell that has aliased to /bin/ls -F, which saves me from having to use the -F flag each time.

The C shell also has conditional statements and a variety of other commands to indicate what commands to run. Here I'm using the if (expression) then to define a set of commands that should be used only when the shell is interactive (that is, I'm going to be able to enter commands). An example of this noninteractive shell is the vi used to create a list when I enter this within the editor. $prompt true if there is a prompt for the shell (that is, if it is interactive). not, the variable is false, and the shell zips to the endif before resuming execution of the commands.

If it is an interactive shell, however, I create a few aliases and define some C shell configuration options, to ensure that the are always set in subshells. The umask value is set, and I then invoke prompt, which is a command alias that runs the command setprompt="$system (cwd) \! :"

> SUMMARY If you're thinking that there is a variety of ways to configure the shell, you are correct. You have an incredibly diverse set of commands in both your .login and .csh files, enabling you to customize many aspects of the C shell and the UNIX environment. You may use either the Bourne or the Korn shell, the configuration information is kept in a similar file called .profile.

![](bbox=[0.075, 0.866, 0.14, 0.966])