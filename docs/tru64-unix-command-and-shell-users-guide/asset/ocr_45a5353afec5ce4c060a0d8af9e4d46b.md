To use rsh, one of the following must be true:

+   - Your local host is listed in the /etc/hosts.equiv file on the remote host.
+   - Your host is listed in the .rhosts file in your home directory on the remote host.

In the following example, rsh appends a file located on a remote host to a file on the local host. The remote file, remfile2, on host remhost2 is appended to a local file called locfile:

```
% rsh remhost2 cat remfile2 >> locfile
```

# 13.3 Using telnet to Log in to a Remote Host

You can log in to a remote host by using the telnet command, which implements the Telnet protocol.

Using telnet you can:

+   - Log in to a remote host
+   - Execute any operating system command on the remote host
+   - Enter telnet subcommands (see Table 13-1) for managing the remote session

The telnet command has the following syntax:

```
telnet [host_name[port]]
```

The host_name variable specifies the remote host. If you omit the host name, you can use the open subcommand to create a connection after you activate the Telnet utility. Example 13-1 shows how to use the telnet command to log in to a remote host named star, use the telnet subcommand status, and close the connection.

If you do not specify a port, the Telnet protocol attempts to contact a Telnet server at the default port.