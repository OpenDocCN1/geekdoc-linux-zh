If you enter no special character before the location entry, `syslogd` assumes that the location is a comma-separated list of users who will have the message written to their screen. If you use an asterisk (*), `syslogd` will send the message to all of the users who are logged in. As usual, any line that begins with a number symbol (#) is a comment. Now take a look at some examples of configuration file entries:

```
# Log all the mail messages in one place.
mail.* /var/log/maillog
```

This example shows that all priorities in the mail facility should have their messages placed in the /var/log/maillog file.
Consider the next example:

```
# Everybody gets emergency messages, plus log them on another
# machine.
*.emerg @loghost,rwhite,bwoodall,root
```

In this example, you see that any facility with a log level of **emerg** is sent to another system running **syslog** called **loghost**. Also, if the user **bwoodall**, **rwhite**, or **root** is logged in, the message being logged is written to the user's console.
You can also specify multiple selectors on a single line for a single event. For example:

```
*.info;mail.none;authpriv.none
/var/log/messages
```

# Using redhat-logviewer

There's nothing wrong with reading a few text files in the /var/log directory, if that's where you have your log messages going. However, you can also use the **redhat-logviewer** utility within a GUI to bring up the pretty interface shown in Figure 8-1.
You can start the utility by typing its name in a terminal window, or by going to the System Tools menu and selecting System Logs. Either way, you'll bring up a window like the one in Figure 8-1. If you customize your log file locations, you can still use the graphical log viewer; just go to the viewer's Edit menu and select Preferences. From there, you can set alert levels and log file paths.