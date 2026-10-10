# Running the Font Server

When you finish setting up font directories and modifying the font server's configuration file, you must start the font server. You can easily start the server on a one-time basis by typing its name, optionally followed by the -daemon parameter to have it run as a daemon:

```
# /usr/X11R6/bin/xfss -daemon
```

At this point, you should be able to configure your local XFree86 to use the font server, as described in the next section, "Using a Font Server." Assuming there are no obstructing firewalls or other network problems, remote systems should also be able to access and use the font server in the same way.

> **Caution** Your font server should not be accessible to all computers on the Internet. You should use a firewall (on the font server computer or another computer), as described in Chapter 17, to restrict access to the font server.

To run xfss on a regular basis, you must have some way to start it. The regular FreeBSD startup scripts don't provide such an option, so you must create an /etc/rc.local or /usr/local/etc/rc.d/xfss.sh script to do the job (the latter is preferred in recent versions of FreeBSD). At its simplest, such a script needs only the startup command presented earlier, but its execute bit must be set. The "Creating New Local Startup Scripts" section of Chapter 6 describes creating such scripts in more detail.

# Using a Font Server

Chapter 13 describes configuring fonts in an X server, and this description includes information on adding a font server to the XP86Config file. Consult Chapter 13 for details; but briefly, you must add a line such as the following to your /etc/X11/XP86Config's Files section:

```
FontPath "tcp/fontserver:7100"
```

In this example, fontserver is the hostname or IP address of the font server computer, and 7100 is the port number on which the server runs. It's best to add this line after your local font directories because local font access is likely to be faster than font server access, and XFree86 tries directories or font servers in the order in which they're listed. After you add this information, the X server will use the font server after you restart X. If you want to use the font server immediately, type the following lines:

```
$ xset fp+ tcp/fontserver:7100
$ xset fp rehash
```