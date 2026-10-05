# GUIDED EXERCISE

# CHANGING THE SHELL ENVIRONMENT

In this exercise, you will use shell variables and variable expansion to run commands and an environment variable to adjust the default editor for new shells.

# OUTCOMES:

You should be able to:

+   - Edit user profile.
- Create a shell variable.
- Create an environment variable.

# BEFORE YOU BEGIN

Log in to workstation as student using student as the password.

On workstation, run ~]$ lab edit-shell start command.

```
$student@workstation ~]$ lab edit-shell start
```

+   1. Change the user's PS1 shell variable to [\u@h \t \w] (remember to put the value of PS1 in quotes and in a trailing space after the dollar sign). This will add the time the prompt was printed to each shell prompt.

+   1.1. On workstation, use the ssh command to log in to server.

```
$student@workstation ~]$ ssh servera
Last login: Wed Jan 23 11:25:05 2019 from 172.25.250.250
$student@servera ~$
```

+   1.2. Use Vim to edit the ~/.bashrc configuration file.

```
$student@servera ~]$ ~/.bashrc
```

+   1.3. Add the PS1 shell variable and its value to the ~/.bashrc file. Remember to include a trailing space at the end of the value you set and put the entire value in quotes, including the trailing space.

```
...output omitted...
# User specific environment and startup programs
PATH=$PATH:$HOME/.local/bin:$HOME
PS1='[\u@h \t \w] '
export PATH
```