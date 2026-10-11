This entry not only denies the host access to the service, but also logs to the auth facility any messages that are severity level info or higher when the denial occurs.

Two useful keywords in the option fields are twist and spawn.

You use the twist keyword when you want to booby-trap what would appear to be a service with another program or action.

For example, if you wanted to cause a message to be sent back to an offending host that tries to use your finger daemon, you might employ the following entry in the /etc/hosts.deny file:

```
in:fingerd: ALL : twist /bin/echo '421 Buzt off!'
```

This sends a standardized message to the host's console telling it access is denied.

The last keyword we'll cover is spawn. Often you'll want to allow some host to connect to a service, but at the same time be notified of the access.

For example, to be notified every time someone accesses telnet so you can email him with an SSH FAQ and scolding note to stop using telnet, you would use the following entry in the access file:

```
in:telnetd: ALL : spawn /bin/echo 'date' from `% | mail root
```

This works for just about any service, as long as it can use the TCP wrappers or can be configured to work from inetd or xinetd.

If you spawn a command, it runs the command as a child of the current shell, but if you use twi st to run the command, it replaces the current process with the command you run.

![](bbox=[0.1, 0.7, 0.2, 0.78])

> Watch carefully for denial file modifications, such as twi st and spawn statements. Being able to verify which entries are valid or invalid is essential.

# sendmail, Bloody sendmail

If there's a topic in the world of Unix and Linux that can cause otherwise competent sysadmins to mutter invectives in frustration, it's sendmail and its configuration files.

Thankfully, you won't have to configure a sendmail server at a level deeper than aliases for users, forwarding email to users, and tools for determining what mail is queued for local and remote delivery.