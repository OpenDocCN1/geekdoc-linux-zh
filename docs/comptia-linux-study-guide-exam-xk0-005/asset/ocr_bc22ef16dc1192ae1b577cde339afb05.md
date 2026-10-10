# FIGURE 8.9 Using local SSH port forwarding with TigerVNC

![](bbox=[0.14, 0.14, 0.85, 0.49])

The \-via localhost option used in conjunction with the vncviewer command forces the connection to use local SSH port forwarding. The last command argument is the destination host's IPv4 address (you could also use a hostname), followed by a colon and the remote desktop's display number (1). This is far easier to use and certainly requires fewer commands and options.

# Remote

The remote SSH port forwarding method starts at the destination host (server), as opposed to the remote client. Therefore, on the destination host, you create the remote desktop secure tunnel with the following command syntax:

```
ssh \-R local\-port:127.0.0.1:remote\-port \-NF user@client\-host
```

There are some important differences in this command from the local method:

+   * The \-R option is used instead of the \-L option.
+   * client\-host is the remote client's IP address or hostname (where you will issue the remote desktop commands).
+   * local\-port is the port number you use on the client\-host with the vncviewer command.
+   * remote\-port is on the remote desktop server.