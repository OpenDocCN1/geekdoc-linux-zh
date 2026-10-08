# 404 TCP/IP BASICS

Besides creation of log files, any other shell command can be issued as. This can be used to procure additional information or to provide the system administrator with information via mail. This can be useful if one wants to gather more information about the remote computer and its users. It does not, however, make much sense to react to an access made with the finger program with a finger in the opposite direction. If both administrators were to do this, both computers would be busy busy.

```
in.tftpd: ALL: (/usr/sbin/safe_finger -l azh | \
/usr/bin/mail -s xd-kh root)
```

**Listing 14.7** Starting shell commands with tcpd.

The example in Listing 14.7 shows one way to start shell commands. You should either use absolute paths or set the PATH variable accordingly. tcpd waits for the end of the command. If you want to allow the connection before that, you must start the shell command in the background by appending an ampersand (&) to the command. In the shell command, you can use some variables that can be substituted with the current values. An overview of these variables can be found in Table 14.1. Please note that not all information is always available; thus, for example, DOS computers do not recognize user IDs.

| Variable | Substitution |
| --- | --- |
| %a | Address of the remote computer |
| %c | user@host, hostname, or address |
| %h | Hostname (or address only) of the computer |
| %d | Name of the daemon to be started |
| %p | Process ID of the daemon |
| %u | User name (or unknown) |
| %% | A single character |

**Table 14.1** Variable substitution by tcpd.

tcpd is a very useful tool as it is easy to configure and flexible in its usage. It helps to make computers a little more secure, especially if you can't install a firewall. But if you have special security requirements, you should install a firewall anyway.