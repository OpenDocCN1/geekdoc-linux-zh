
## Appendix A Implementing Cybercrime Detection Techniques on Windows and *nix

### Figure A.2 Security Log Showing Events for Which Auditing Is Enabled

| ID | Date | Time | Source | Category | Event | User | Computer |
|---|---|---|---|---|---|---|---|
| Success Audit | 2009/01/11 | 12:25:25 AM | Security | Privilege | 576 | LOCAL SERVICE | 06-2009 |
| Success Audit | 2009/01/11 | 12:25:29 AM | Security | Logonoff | 528 | LOCAL SERVICE | 06-2009 |
| Failure Audit | 2009/01/11 | 12:25:39 AM | Security | Account Logon | 600 | SYSTEM | 06-2009 |
| Success Audit | 2009/01/11 | 12:25:45 AM | Security | Privilege | 576 | NETWORK SERVICE | 06-2009 |
| Success Audit | 2009/01/11 | 12:25:49 AM | Security | Logonoff | 529 | NETWORK SERVICE | 06-2009 |
| Failure Audit | 2009/01/11 | 12:25:01 AM | Security | Privilege | 576 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:25:02 AM | Security | Logonoff | 529 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:25:03 AM | Security | Account Logon | 600 | SYSTEM | 06-2009 |
| Success Audit | 2009/01/11 | 12:24:54 AM | Security | Privilege | 576 | Administrator | 06-2009 |
| Success Audit | 2009/01/11 | 12:24:55 AM | Security | Logonoff | 528 | Administrator | 06-2009 |
| Failure Audit | 2009/01/11 | 12:24:56 AM | Security | Privilege | 576 | NETWORK SERVICE | 06-2009 |
| Failure Audit | 2009/01/11 | 12:24:57 AM | Security | Logonoff | 529 | NETWORK SERVICE | 06-2009 |
| Failure Audit | 2009/01/11 | 12:24:58 AM | Security | Account Logon | 600 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:24:59 AM | Security | System-Period | 515 | SYSTEM | 06-2009 |
| Success Audit | 2009/01/11 | 12:24:00 AM | Security | Logonoff | 528 | Administrator | 06-2009 |
| Success Audit | 2009/01/11 | 12:24:01 AM | Security | Account Logon | 600 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:24:02 AM | Security | Logonoff | 529 | NETWORK SERVICE | 06-2009 |
| Failure Audit | 2009/01/11 | 12:24:03 AM | Security | Account Logon | 600 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:23:46 AM | Security | Logonoff | 529 | NETWORK SERVICE | 06-2009 |
| Failure Audit | 2009/01/11 | 12:23:47 AM | Security | Account Logon | 600 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:23:48 AM | Security | Logonoff | 529 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:23:49 AM | Security | Account Logon | 600 | SYSTEM | 06-2009 |
| Failure Audit | 2009/01/11 | 12:23:50 AM | Security | Logonoff | 529 | NETWORK SERVICE | 06-2009 |

The profound trade-offs between auditing and system performance are manifested in least two ways:

- The more objects and activities that are audited, the more impact that the collection and recording of such data will have on system performance and consumption of disk space (because all of those logged activities are written to files on disk).
- The more objects and activities that are audited, the more administrators and investigators will have to dig through to find items of interest among routine or benign events.

If a large amount of data is collected, however, all is lost. You can configure the Event Viewer to filter logged events so that only certain event types (for example, only failures) or only events that originate with specific sources, users, or computers are displayed. Other options include displaying only events that occur on a specified date/or time or within a specified period, or events in a certain category or marked with a specific event ID. Figure A.3 shows the dialog box that is used to configure display filtering.

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_210_0.png)

### Figure A.3 Configuring Display Filtering to Display Only Specified Logged Events

### ### Designing Effective Audit Strategies

### Table A.2 Common Syslog Facilities

| Facility | Description |
| --- | --- |
| Auth | Authorization systems (for example, login and su) |
| Cron | The cron daemon drives scheduled scripts and executes them as scheduled. |
| Daemon | Miscellaneous daemons not covered by other facilities |
| Kern | Abbreviation of system kernel—the operating system's memory-resident core code |
| local0-local7 | Reserved for local use (numbered 0 through 7) |
| Lpr | Print spooling (line printer remote) system |
| Mark | A timestamp service that emits a timestamp for logging every 20 minutes (1,200 seconds) |
| Mail | E-mail system |
| Syslog | Internal syslog data |

### ### On the Scene

Ultimately, what the administrator chooses to audit depends on the kinds of activity that occur on the server or device, the kinds of attacks or intrusions anticipated, and the kinds of information or assets the organization seeks to monitor (and protect). Thus, it might make sense to audit specific signatures at the periphery of the network (on firewalls, routers, application gateways, and forth). But sensitive files reside, probably makes sense to audit access to, including attempted and successful accesses that IT professionals know will be held accountable for all official (and unsanctioned) administrative activities they perform. In some situations—perhaps when an account is compromised—it may make sense to disable that account (and set up a new account for the account's user), and then audit subsequent attempts to use the old account. This permits administrators to determine whether such activity originates inside or outside the network boundary. The general principle at work here is to audit for suspicious activities, to track administrative activity, and monitor information or assets of value or interest. By combining these activities into the auditing strategy, it's easier to strike the right balance between audit data volume and the amount of useful information that can be discerned from data.

### Auditing for UNIX and Linux Platforms

Every different distribution and version of UNIX logs audit information in its own way and stores the resultant log files in particular locations using specific default formats. Nevertheless, most UNIX and Linux operating systems support extensive logging capabilities and share numerous features.

The Syslog daemon (syslogd) is a clearinghouse for all kinds of log information on UNIX and Linux systems. The daemon is a process that directs different system messages to different files, depending on the type of message and how urgent it is. For example, on a FreeBSD system, successful and failed File Transfer Protocol (FTP) logons are shown in the ftp.log file, information about access to Apache Web sites is stored in access_log, and information about failed logons resides in secure.log.

Most networks that incorporate UNIX or Linux systems also set up special network drives to record logging data, so it can all reside in a single centralized location. In addition, the Syslog daemon receives event data from various operating system and user applications (listed in Table A.2); it also stores all log data using a single standardized format for easy interpretation and analysis. (The same consistency, alas, is not found for all logs on Windows systems, where the Event Viewer uses one format for its logs, but other applications and services use other formats.)

In fact, Syslog prioritizes event or error messages to a predefined scheme (listed in Table A.3). Higher-priority messages appear at the top of this table, and lower-priority messages appear at the bottom of this table.

As mentioned previously, various UNIX or Linux log files store particular types of events or information. Thus, the login records failed login attempts, and the sul records su (superuser) command activity and identifies the user account where the activity originated. The utmp log identifies all users who are currently logged on to a system, and the wtmp log stores snapshots of utmp information at regular intervals. These are only some of the many log files you'll find on most Linux and UNIX systems; please consult your system documentation and man pages to obtain a complete listing of logging facilities, formats used, and (default) storage locations.

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_213_0.png)
