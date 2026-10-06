# The /etc/inititab File

The options +min and -t sec can be used with the -h argument of the
shutdown command.

The /etc/inititab file determines the processes that should be active at
each level. Lines in the file have the form

```
id:runlevels:action:process
```

The fields are as follows:

+   id, a 1-4 character unique identification. For login processes, id
should be the tty suffix of the corresponding tty.

+   runlevels, a list of runlevels for which the action should be taken. If
omitted, the action is taken for each runlevel.

+   action, which specifies the action to be taken. Table 15.7 summarizes
the available actions.

+   process, which specifies the program to be executed.

Lines beginning with a hash mark (#) are ignored.

# TABLE 15.7 Actions Specifiable in /etc/inititab

| Action | Description |
|---|---|
| boot | The specified process is executed during system boot. The runlevels field is ignored. |
| bootwait | The process is executed during system boot; init waits for its termination. The runlevels field is ignored. |
| ctraltdel | The process is executed when init receives the SIGINT signal, meaning that someone on the system console has pressed the Ctrl+Alt+Del key combination. |
| initdefault | Specifies the initial runlevel, which is entered after system boot. The process field is ignored. |
| krequest | The process is executed when init receives a signal from the keyboard handler that a special key combination was pressed on the console keyboard. |
| off | No action taken. |