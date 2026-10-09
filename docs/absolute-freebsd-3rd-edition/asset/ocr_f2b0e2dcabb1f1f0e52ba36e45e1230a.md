> If you’re using a lot of options, wrapper rules can get very long. To help keep rules readable, the *hosts.allow* file can use the backslash (\) followed by a return as a line-continuation character.

# ## Logging

Once you’ve decided to accept or reject the connection attempt, you can also log the connection. Suppose you want to permit but specifically log all incoming requests from a competitor. Similarly, you might want to know how many connections your server rejects because of DNS problems when using the *PARANOID* client keyword. Logging is good. More logging is better. Disk space is cheaper than your time.

The *severity* option sends a message to the system log, *syslogd(8)*. You can configure *syslogd* to direct these messages to an arbitrary file based on the *syslogd* facility and level you choose (see Chapter 21).

```
sshd: ALL: severity local0.info: allow
```

This example permits all SSH connections but also logs them using the *local0* facility.

# ## Twisting

The *twist* option allows you to run arbitrary shell commands and scripts when someone attempts to connect to a wrapped TCP daemon and returns the output to the remote user. The *twist* option works properly only with TCP connections. (Remember, UDP is connectionless; there’s no connection to return the response over, so you must jump through very sophisticated and annoying hoops to make *twist* work with UDP. Also, protocols that transmit over UDP frequently don’t expect such a response and aren’t usually equipped to receive or interpret it. Using *twist* with UDP isn’t worth the trouble.) The *twist* option takes a shell command as an argument and acts as a deny-plus-do-this rule. You must know basic shell scripting to use *twist*; very complicated uses of *twist* are possible, but we’ll stick with the simple ones.