
The basic idea behind a system logger is to provide a unified means of handling log files. The daemon runs in the background and accepts data delivered from servers and other programs that are configured to use the log daemon. The daemon can then use information provided by the server to classify the message and direct it to an appropriate log file. This configuration enables you to consolidate messages from various servers in a handful of standard log files, which can be much easier to use and manage than potentially dozens of log files from the various services running on the system.

As described in the upcoming section “Using a Remote Server for Log Files,” another feature of log daemons is that they can pass the log information on to a log daemon running on another computer entirely. The advantage of this configuration is that it can help protect the logs from tampering—if a computer is compromised, the intruder can’t eliminate evidence of the intrusion from the log file without first breaking into the computer that logs data for other systems. Administering a network on which all systems log to a single system can also be simpler in some ways, because you can monitor log files on one computer, rather than perform this task on many systems.

In order to work, of course, the log daemon must be configured. In the case of syslogd, this is done through the /etc/syslog.conf file. The next section describes this file’s format in more detail.

## Setting Logging Options

The format of the /etc/syslog.conf file is conceptually simple but provides a great deal of power. Comment lines, as in many Linux configuration files, are denoted by a hash mark (#). Noncomment lines take the following form:

```
facility.priority action
```

In this line, *facility* is a code word for the type of program or tool that has generated the message to be logged; *priority* is a code word for the importance of this message; and *action* is a file, remote computer, or other location that’s to accept the message. The facility and priority are often referred to collectively as the *selector*.

Valid codes for *facility* are *auth*, *authpriv*, *cron*, *daemon*, *kern*, *lpr*, *mail*, *mark*, *news*, *security*, *syslog*, *user*, *ucsp*, and *local0* through *local7*. Many of these names refer to specific servers or program classes. For instance, mail servers and other mail-processing tools typically log using the *mail* facility. Most servers that aren’t covered by more specific codes use the *daemon* facility. The *security* facility is identical to *auth*, but *auth* is the preferred name. The *mark* facility is reserved for internal use. An asterisk (*) refers to all facilities. You can specify multiple facilities in one selector by separating the facilities with commas (,).

Valid codes for *priority* are *debug*, *info*, *notice*, *warning*, *warn*, *error*, *err*, *crit*, *alert*, *emerg*, and *panic*. The *warning* priority is identical to *warn*, *error* is identical to *err*, and *emerg* is identical to *panic*. The *error*, *warn*, and *panic* priority names are deprecated; you should use their equivalents instead. Other than these identical pairs, these priorities represent ascending levels of importance. The *debug* level logs the most information; it’s intended, as the name implies, for debugging programs that are misbehaving. The *emerg* priority logs the most important messages, which indicate very serious problems.

When a program sends a message to the system logger, it includes a priority code; the logger logs the message to a file if you’ve configured it to log messages of that level or higher. Thus, if you specify a *priority* code of *alert*, the system will log messages that are classified as *alert* or *emerg*, but not messages of *crit* or below. An exception to this rule is if you precede the priority code by an equal sign (*=*,) as in *"=crit"*, which describes what to do with messages of *crit* priority only. An exclamation mark (!) reverses the meaning of a match. For instance, `!crit` causes messages *below* *crit* priority to be logged. A priority of * refers to all priorities.

You can specify multiple selectors for a single action by separating the selectors by a semicolon (;). Examples appear shortly.

Most commonly, *action* is a filename, typically in the */var/log* directory tree. Other possibilities include a device filename for a console (such as `/dev/console`) to display data on the screen, a remote machine name preceded by an at-sign (@), and a list of usernames who should see the message if they’re logged in. For the last of these options, an asterisk (*) means all logged-in users.

Some examples should help clarify these rules. First is a fairly ordinary and simple entry:

```
mail.*                 /var/log/mail
```

This line sends all log entries identified by the originating program as related to mail to the `/var/log/mail` file. Most of the entries in a default `/etc/syslog.conf` file resemble this one. Together, they typically cover all of the facilities mentioned earlier. Some messages may be handled by multiple rules. For instance, another rule might look like this one:

```
*.*emerg              *
```

This line sends all *emerg*-level messages to the consoles of all users who are logged into the computer using text-mode roots. If this line and the earlier `mail.*` selector are both present, *emerg*-level messages related to mail will be logged to `/var/log/mail` *and* displayed on users’ consoles.

A more complex example logs kernel messages in various ways, depending on their priorities:

```
kern.*               /var/log/kernel
kern.crit            @logger.pangaea.edu
kern.crit            /dev/console
kern.info;kern.err   /var/log/kernel-info
```

The first of these rules logs all kernel messages to `/var/log/kernel`. The next two lines relate to high-priority (*crit* or higher) messages from the kernel. The first of these lines sends such messages to `logger.pangaea.edu`. (The upcoming section “Using a Remote Server for Log Files” describes remote logging in more detail.) The second of these lines sends a copy of these messages to `/dev/console`, which causes them to be displayed on the computer’s main text-mode console display. Finally, the last line sends messages that are between *info* and *err* in priority to `/var/log/kernel-info`. Because *err* is the priority immediately above *crit* and because *info* is the lowest priority, these four lines cause all kernel messages to be logged two or three times: once to /var/log/kernel as well as to either the remote system and the console or to /var/log/kernel-info.

Most distributions ship with reasonable system logger settings, but you may want to examine these settings and perhaps adjust them. If you change them, though, be aware that you may need to change some other tools. For instance, all major distributions ship with tools that help rotate log files. If you change the files to which syslogd logs messages, you may need to change your log file rotation scripts as well.

In addition to the system logger’s options, you may be able to set logging options in individual programs. For instance, you might tell programs to record more or less information or to log routine information at varying priorities. Some programs also provide the means to log via the system log daemon or via their own mechanisms. Details vary greatly from one program to another, so you should consult the program’s documentation for details.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_205_0.png)

Most programs that use the system log daemons are servers and other system tools. Programs that individuals run locally seldom log data via the system log daemon, although there are some exceptions to this rule, such as the Fetchmail program for retrieving e-mail from remote servers.

## Rotating Log Files

Log files are intended to retain information on system activities for a reasonable period of time; however, system logging daemons provide no means to control the size of log files. Left unchecked, log files can therefore grow to consume all the available space on the partition on which they reside. To avoid this problem, Linux systems employ log file rotation tools. These tools rename and optionally compress the current log files, delete old log files, and force the logging system to begin using new log files.

The most common log rotation tool is a package called logrotate. This program is typically called on a regular basis via a cron job. (Cron jobs are described in Chapter 3.) The logrotate program consults a configuration file called /etc/logrotate.conf, which includes several default settings and typically refers to files in /etc/logrotate.d to handle specific log files. A typical /etc/logrotate.conf file includes several comment lines, denoted by hash marks (#), as well as lines to set various options, as illustrated by Listing 4.2.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_205_1.png)

Because log file rotation is handled by cron jobs that typically run late at night, it won’t happen if a computer is routinely turned off at the end of the day. This practice is common with Windows workstations, but is uncommon with servers. Either Linux workstations should be left running overnight as a general practice or some explicit steps should be taken to ensure that log rotation occurs despite routine shutdowns. You might leave the system up overnight from time to time, for instance, or reschedule the log rotation to some time when the computer is likely to be powered on. The Anacron package (http://anacron.sourceforge.net) is another option; it supplements cron by running programs at intervals even when the computer isn’t up at specific times.
