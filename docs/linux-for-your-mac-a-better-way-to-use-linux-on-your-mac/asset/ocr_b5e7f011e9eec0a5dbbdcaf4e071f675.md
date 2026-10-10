# Customizing the Shell Prompt

Your shell’s prompt is defined by one or more environment variables. When using the bash shell, the value of the PS1 variable defines the first login prompt. This value, defined by default by your system’s /etc/profile determines what kind of information is displayed in your shell prompt.

You can use the printenv command, along with the fgrep command, to display the current prompt definition like this:

```
$ printenv | fgrep PS1
```

You may see the following value returned:

```
PS1=\u@h:\w >
```

This example from a SuSE Linux system indicates that the shell prompt should be the user’s name, then the at symbol (@), followed by the hostname of the computer, a colon (.), the current working directory, and finally, a greater than (-) symbol. This will look like:

```
bball@cubie: ~ >
```

Note in this example that the home directory is shown as a tilde (~). Read the bash manual page to see a list of predefined values you can use for your shell prompt. Some of the more commonly used variables are:

| \d The date in “Wed March 07” format |
| --- |
| \h, \H Host name of the computer |
| \s Name of the shell |
| \t The time in 24-hour format |
| \T The time in 12-hour format |
| \u Username |
| \w Current working directory |
| \W Basename of the current working directory |
| \# Number of this command |
| \\ A backslash |

You can redefine your shell prompt by redefining or exporting your shell’s prompt variable. For example, if you use bash and would rather see the time updated after every command, use bash’s export command like this:

```
$ export PS1='It is now: \t $ '
```