> **Caution** Be careful with the `LOCAL` command. If your `/etc/hosts` file contains an entry with just a host name and no domain, it may be *allowed* access whether it is actually local or not.

The optional shell command can be used to perform a function when a client connects that matches the specified rule. A number of patterns can be used in the shell command that are expanded out when run. Table 17-2 lists these patterns. Another useful option is the `twist` command. This causes the output of the shell command to be shown to the connecting client, along with any information from the expansion patterns. For example:

```
```
in.telnetd : .evil.org : twist /bin/echo "Sorry &c, but we
don't want your kind around here."
```
```

This would cause the message to be echoed out to any user from the `evil.org` domain connecting to the Telnet server.

**Table 17-2 tcpd Patterns**

| Pattern | Function |
| :--- | :--- |
| %a | The connecting client's host address. |
| %A | The server's host address. |
| %c | Client information such as user@host, user@address, hostname, or address depending on what is available. |
| %d | The daemon process name. |
| %h | The connecting client's hostname, or address if the host cannot be retrieved. |
| %H | The server's hostname, or address if the host cannot be retrieved. |
| %n | The client hostname. |
| %N | The server hostname. |
| %p | The daemon's process ID. |
| %s | Server information such as daemon@host, daemon@address, or just the daemon name depending on what is available. |
| %u | The client user name, or unknown. |

TCP wrappers provide a couple of utilities to check your configuration. The first is `tcpschk`. It is used to check your syntax and make sure the rules do what you are expecting. Table 17-3 lists the `tcpschk` command-line options. The following is sample output from `tcpschk`.