The Scenario, presented earlier, specifies that emergency log events should be displayed to all currently logged-in users and that kernel messages should be logged in `/var/log/kernel` and non-trivial kernel events should be sent to a second system (`logger.pangaea.edu`). To begin with the first requirement, you should create this entry in `/etc/syslog.conf`:

```
* .emerg *
```

This line sends all **emerg-level** messages to the consoles of all users who are logged into the computer using text-mode tools. If a message matches both this specification and another one (probably an existing rule), such events will be logged in the way specified by the existing rule *and* displayed on users’ consoles.

The second Scenario requirement is to log kernel messages to `/var/log/kernel` and non-trivial kernel events to a second system, `logger.pangaea.edu`. To do so, you’d create entries like this:

```
kern.* /var/log/kernel
kern.err @logger.pangaea.edu
```

![](bbox=[0.14, 0.5, 0.23, 0.55])

> The specification in the Scenario was a bit vague: What constitutes a “non-trivial” kernel message? For purposes of this task, I’ve used *err* as the cutoff point, but you could legitimately use just about any other priority code.

The first of these rules logs all kernel messages to `/var/log/kernel`. (It’s possible that your configuration already sends kernel messages to this or some other file, so check to see if you’re duplicating functionality before making changes.) The next line sends *err*-level messages to `logger.pangaea.edu`. (This system must be configured to accept remote logs, which is a topic not covered in this book.)

Most distributions ship with reasonable system logger settings, but you may want to examine these settings and perhaps adjust them. If you change them, though, be aware that you may need to change some other tools. For instance, all major distributions ship with tools that help rotate log files. If you change the files to which *syslog* logs messages, you may need to change your log file rotation scripts as well. This topic is covered in the next section.

In addition to the system logger’s options, you may be able to set logging options in individual programs. For instance, you might tell programs to record more or less information or to log routine information at varying priorities. Some programs also provide the means to log via the system log daemon or via their own mechanisms. Details vary greatly from one program to another, so you should consult the program’s documentation for details.

![](bbox=[0.14, 0.9, 0.23, 0.95])

> Most programs that use the system log daemons are servers and other system tools. Programs that individuals run locally seldom log data via the system log daemon, although there are some exceptions to this rule, such as the Fetchmail program for retrieving email from remote servers.