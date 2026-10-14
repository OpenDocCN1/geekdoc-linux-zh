Eliminating the defaultroute and proxyarp options ensures that users will be able to access only the SuSE Linux server—meaning they will only be able to grab their emails or FTP to the SuSE Linux server.

For users whom you want to be able to access the Internet through SuSE Linux, add the following lines to the .ppprc that resides in their home directories:

```
defaultroute
proxyarp
```

# Troubleshooting

*I can't dial in to my SuSE Linux. It does not answer. Why is that?*

This might be due to several reasons:

+   - mgetty isn't running or was run by hand. Make sure that mgetty has an entry in the /etc/inittab file as discussed in this chapter.
+   - mgetty isn't configured on the correct modem port. Review your configuration and make sure that mgetty is listening to the correct port.
+   - Make sure the number you are dialing in isn't one of the disallowed numbers if you have a caller ID installed.

*I'm trying to establish a connection through the terminal. The connection dies when I start pppd.*

This is an /etc/options misconfiguration. Some people need to have the -detach option in this file.

*I can't see any machine beyond the server. Why is that?*

The /etc/options file needs to have the following lines to make a route entry for the client:

```
defaultroute
proxyarp
```