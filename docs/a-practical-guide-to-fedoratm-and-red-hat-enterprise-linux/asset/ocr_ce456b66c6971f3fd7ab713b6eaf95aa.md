If you omit the argument to `ssh-add`, it adds a passphrase for each of the `~/.ssh/id_rsa`, `~/.ssh/id_dsa`, and `~/.ssh/identity` files that exist.

With this setup, you can use `ssh` to work on a remote system without supplying a login password and by supplying your passphrase one time per session.

# COMMAND-LINE OPTIONS

Command-line options override declarations in the configuration files. Following are descriptions of some of the more useful `sshd` options.

+   - `-D (noDetach)` Keeps `sshd` in the foreground. Useful for debugging; implied by `-d`.

+   - `-d (debug)` Sets debug mode so that `sshd` sends debugging messages to the system log and the server stays in the foreground (implies `-D`). You can specify this option a maximum of three times to increase the verbosity of the output. See also `-e`. (The `ssh` client uses `-v` for debugging; page 695.)

+   - `-e (error)` Sends output to standard error, not to the system log. Useful with `-d`.

+   - `-f file` Specifies *file* as the configuration file instead of `/etc/ssh/sshd_config`.

+   - `-t (test)` Checks the configuration file syntax and the sanity of the key files.

# /etc/ssh/sshd_config CONFIGURATION FILE

Lines in the `/etc/ssh/sshd_config` configuration file contain declarations. Each of these declarations starts with a keyword that is not case sensitive. Some keywords must be followed by whitespace and one or more case-sensitive arguments. You must reload the `sshd` server before these changes will take effect.

**AllowUsers userlist**

The `userlist` is a SPACE-separated list of usernames that specifies which users are allowed to log in using `sshd`. This list can include `*` and `?` wildcards. You can specify a user as `user` or `user@host`. If you use the second format, make sure you specify the host as returned by `hostname`. Without this declaration, any user who can log in locally can log in using an OpenSSH client. Does not work with numeric user IDs.

**ClientAliveCountMax n**

The *n* specifies the number of client-alive messages that can be sent without receiving a response before `sshd` disconnects from the client. See `ClientAliveInterval`. Default is 3.

**ClientAliveInterval n**

Sends a message through the encrypted channel after *n* seconds of not receiving a message from the client. See `ClientAliveCountMax`. The default is 0, meaning that no messages are sent.

This declaration passes messages over the encrypted channel (application layer; page 291) and is not susceptible to IP *spoofing* (page 1256). It differs from `TCPKeePalive`, which uses the TCP `keealive` option (transport layer; page 291) and is susceptible to IP *spoofing*.