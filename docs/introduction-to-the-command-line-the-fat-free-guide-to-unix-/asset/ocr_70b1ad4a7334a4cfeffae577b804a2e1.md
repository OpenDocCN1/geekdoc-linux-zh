# # sudo

Purpose: Run a single command as a different user.

Usage syntax: `sudo [OPTIONS] [COMMAND]`

```
$ whoami
nick
$ sudo whoami
[sudo] password for nick: ******
root
$ whoami
nick

Using sudo to run a command as the root user
```

The `sudo` command allows you to run a single command as another user. It is most commonly used to execute commands that require root privileges. In this example `whoami` is executed as root via the `sudo` command.

Using the `sudo` command is the recommended way to run commands that require elevated privileges as it limits the amount of time spent with root privileges. This greatly helps prevent disasters such as accidental deletion of important system files.

> **Note**
> User (or group) accounts must be listed in the /etc/sudoers file in order to execute commands as root with sudo.

Common usage examples:

+   `sudo [COMMAND]` → Run the specified command as root
+   `sudo -u [USER] [COMMAND]` → Run a command as the specified user
+   `sudo !!` → Run the last command as root