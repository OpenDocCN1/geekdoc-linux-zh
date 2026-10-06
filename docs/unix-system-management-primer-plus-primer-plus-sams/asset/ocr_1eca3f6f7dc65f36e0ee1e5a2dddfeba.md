# Aliases

The aliases section of sudoers alows you to define named lists of users, hosts, and commands for future reference. There are four types of aliases lists:

+   * User_Alias Users who can run commands with sudo
* Runas_Alias Users a command can run as
* Host_Alias Hosts on which you can run commands with sudo
* Cmd_Alias Commands that can be run with sudo

An alias is defined as follows:
Alias_Type NAME = item1, item2, ..., itemN

As an example, you can define a list of commands that a backup operator would run with this line:
Cmnd_Alias BACKUP_COMMANDS = /usr/lib/ufs/fsdump, /usr/lib/ufs/ufsfs,, /usr/bin/tar

![](bbox=[0.148, 0.403, 0.198, 0.442])

Allow Users to Run Every Command in a Directory
You can include all of the commands in a directory Cmnd_Alias by appending a slash to the directory name (for example, /usr/local/bin/). This is much easier than typing each individual command into the sudoers file.

# Defaults

The defaults section allows you to alter sudo's default settings in some very flexible ways. sudo contains too many default settings to list here, but some of the more interesting ones are follows:

+   * timestamp_timeout Time between password requests
* logfile Path to fileto send logs (sudo logs to syslog by default)
* mailto Address to send error and warning messages (these messages are sent to root by default)

Defaults are set like many aliases; for example, the following configuration sets the timestamp to 15 minutes instead of the default 5 minutes:

```
Defaults timestamp_timeout=15
```

# User Specification

The user specification section is where you actually specify what commands a user can run, and as what user person can run the commands. The syntax in this section can be a bit confusing, but it basically looks like this:

```
ID HOST = (USER) COMMANDS
```