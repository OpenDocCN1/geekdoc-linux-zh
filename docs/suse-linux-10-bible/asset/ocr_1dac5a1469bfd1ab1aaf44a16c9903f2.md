name of the machine that the message originated from (in this case, bible). The next entry is usually the process that actually created the log entry (in this case the ssh daemon). The number you see next to the process name is the process number, followed by the message itself.

The message you see in this example is self-explanatory, saying that there was an authentication error. The PAM: entry is something you will see with authentication errors in Linux (Pluggable Authentication Modules) is used to take a username and password for a process and decide if this user with the password they have entered is actually to log in the system.

This example is an informational message from the kernel after a kernel driver has loaded:

```
May 27 22:19:22 bible kernel: IPv6 over IPv4 tunneling driver
```

This means that the driver that deals with tunneling IPv6 traffic over IPv4 has been loaded successfully.

So here you have seen two extremes of what you might find in a log file. The latter example is a general informational message telling you that all is fine. The other is a bit serious, telling you that someone attempted to log in to the system but failed because they provided the wrong authentication information (wrong username or password).

Log files are there to help you in your running of your Linux system. You have to be vigilant in your efforts to keep the system running nicely, and log files help you with this.

Have you checked your logs?