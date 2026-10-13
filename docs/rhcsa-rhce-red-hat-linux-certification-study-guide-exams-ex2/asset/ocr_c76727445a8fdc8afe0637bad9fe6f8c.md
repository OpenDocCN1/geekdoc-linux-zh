For more information, see www.rsyslog.com/doc/imudp.html and www.rsyslog.com/doc/imtcp.html.

# ### UDP Directives

The standard suggested UDP directive specifies the port number where the server listens for logging clients:

```
$UDPServerRun 514
```

If there are multiple network cards on the local system, the following directive limits the logging server to the noted IP address:

```
$UDPServerAddress 192.168.122.50
```

# ### TCP Directives

As with UDP, the standard suggested TCP directive specifies the port number where the server listens for logging clients. Multiple port numbers are supported, for configurations where you want to set up support for multiple clients.

```
$InputTCPServerRun 514
```

You can configure rsyslog to send a message if a logging client closes a connection:

```
$InputTCPServerNotifyOnConnectionClose on
```

If this server is working with a number of clients on different ports, you can use the **$InputTCPMaxListeners** directive to increase the number of such ports beyond the default of 20. This can work with the following directive, which sets the maximum number of supported sessions (the default is 200):

```
$InputTCPMaxSessions
```

If you set a nondefault value of **$InputTCPMaxSessions**, that directive must be set before directives such as **$InputTCPServerRun 514**.

# ## Configure Logging Clients

One of the features of the default rsyslog.conf file is the group of comments shown in Figure 17-7.