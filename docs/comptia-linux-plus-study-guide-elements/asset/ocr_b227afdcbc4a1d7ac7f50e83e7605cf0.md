The basic idea behind a system logger is to provide a unified means of handling log files. The daemon runs in the background and accepts data delivered from servers and other programs that are configured to use the log daemon. The daemon can then use information provided by the server to classify the message and direct it to an appropriate log file. This configuration enables you to consolidate messages from various servers in a handful of standard log files, which can be much easier to use and manage than potentially dozens of log files from the various services running on the system.

As described in the upcoming section “Using a Remote Server for Log Files,” another feature of log daemons is that they can pass the log information on to a log daemon running on another computer entirely. The advantage of this configuration is that it can help protect the logs from tampering—if a computer is compromised, the intruder can’t eliminate evidence of the intrusion from the log file without first breaking into the computer that logs data for other systems. Administering a network on which all systems log to a single system can also be simpler in some ways, because you can monitor log files on one computer, rather than perform this task on many systems.

In order to work, of course, the log daemon must be configured. In the case of syslogd, this is done through the /etc/syslog.conf file. The next section describes this file’s format in more detail.

# # Setting Logging Options

The format of the /etc/syslog.conf file is conceptually simple but provides a great deal of power. Comment lines, as in many Linux configuration files, are denoted by a hash mark (#). Noncomment lines take the following form:

```
facility.priority action
```

In this line, *facility* is a code word for the type of program or tool that has generated the message to be logged; *priority* is a code word for the importance of this message; and *action* is a file, remote computer, or other location that’s to accept the message. The facility and priority are often referred to collectively as the *selector*.

Valid codes for *facility* are *auth*, *authpriv*, *cron*, *daemon*, *kern*, *lpr*, *mail*, *mark*, *news*, *security*, *syslog*, *user*, *ucsp*, and *local0* through *local7*. Many of these names refer to specific servers or program classes. For instance, mail servers and other mail-processing tools typically log using the *mail* facility. Most servers that aren’t covered by more specific codes use the *daemon* facility. The *security* facility is identical to *auth*, but *auth* is the preferred name. The *mark* facility is reserved for internal use. An asterisk (*) refers to all facilities. You can specify multiple facilities in one selector by separating the facilities with commas (,).

Valid codes for *priority* are *debug*, *info*, *notice*, *warning*, *warn*, *error*, *err*, *crit*, *alert*, *emerg*, and *panic*. The *warning* priority is identical to *warn*, *error* is identical to *err*, and *emerg* is identical to *panic*. The *error*, *warn*, and *panic* priority names are deprecated; you should use their equivalents instead. Other than these identical pairs, these priorities represent ascending levels of importance. The *debug* level logs the most information; it’s intended, as the name implies, for debugging programs that are misbehaving. The *emerg* priority logs the most important messages, which indicate very serious problems. When a