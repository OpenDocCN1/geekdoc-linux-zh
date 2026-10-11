+   - —A minus sign is used to prefix a target file to indicate that syslogd shouldn't flush the buffers to disk after a write. This improves performance, but if the system crashes, some logs might be lost.

# # Putting It All Together

Now that we've defined where logging is configured, what logging does, what facilities and levels are, and what an action and a specifier is, it's time to put all this together. Remember that you're in the `syslog.conf` file and configuring where the system log entries will be sent to.

The following are examples that occur in the real world or make a good point. I've attempted to cover every instance that might occur on the exams. The examples are arranged from simplest to most complex.

# ## Syslog Entry Examples

To log every facility at every priority level except debug to a log file, you'd use the following:

```
```
*.*                /var/log/somelog
```
```

To log all user facility messages of warning and higher to a file named `/var/log/user.log`, you'd use the following:

```
```
user.warning     /var/log/user.log
```
```

To log all messages of info or higher priority from the user facility to all logged in users, you'd use this:

```
```
user.*               *
```
```

> NOTE  If a user is listed as a target and isn't logged in, the message isn't sent and no extra errors are logged as a result of the message being undeliverable.

To log all messages from the auth and daemon facilities to the console of the root user, if logged on, you'd use this:

```
```
auth.*;daemon.*     root
```
```

To log all auth messages except emerg to the console of the root user if he's logged on, you'd use the command shown here:

```
```
auth.!emerg     root
```
```