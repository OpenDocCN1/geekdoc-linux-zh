# lastcomm 625

See Also
utmpx(4), attributes(5)

# lastcomm - Display the Last Commands Executed, in Reverse Order

# Synopsis

```
/usr/bin/lastcomm [-f file] [-x] [command-name]... [user-name]...
(terminal-name)...
```

# Description

The lastcomm command shows information about previously executed accounting commands that are stored in /var/adm/pacct file. lastcomm with no arguments displays information about all the commands recorded during the current accounting file's lifetime. If you specify arguments, lastcomm displays only entries with a matching command-name, user-name, or terminal-name.

If extended accounting is active, lastcomm tries to take data from the extended process accounting file, and is recording the appropriate data (acct(1M)) (New!). If standard process accounting is active, lastcomm takes data from the current standard accounting file (acct(2)).

If terminal-name is -, there was no controlling TTY for the process. The process was probably executed during boot time. If terminal-name is ??, the controlling TTY could not be decoded into a printable name.

For each process entry, lastcomm displays the following information:

+   * The command name under which the process was called.
* One or more flags indicating special information about the process. The flags have the following meanings:
  * F The process performed a fork but not exec.
  * S The process ran as setuid program.
* The name of the user who ran the process.
* The terminal where the user was logged in at the time (if applicable).
* The amount of CPU time used by the process (in seconds).
* The date and time the process exited.

# Options

-f file Use file as the source of accounting data. filecan be either an extended process accounting file or a standard process accounting file. New in the Solaris 8 release.

-x Use the currently active extended process accounting file. If extended process accounting is inactive, lastcomm produces output. New in the Solaris 8 release.