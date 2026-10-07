
# Table A.3 Syslog Priorities

| Priority | Description |
|---|---|
| Emerg | Panic conditions broadcast to all users |
| Alert | Conditions requiring immediate intervention |
| Crit | Critical errors, such as a device failure |
| Err | Standard priority errors |
| Warning | Warning messages |
| Notice | Notifications that may require some action or response |
| Info | Informational messages |
| Debug | Shows messages written to Syslog when programs run in debug mode |

# Firewall Logs, Reports, Alarms, and Alerts

Because firewalls sit on the boundary between internal and external networks, they're ideally positioned to observe incoming (and outgoing) traffic. Thus, it should come as no surprise that firewalls not only represent a first and most important line of defense to foil or deflect attack, but also that you can configure them to monitor and track activity that can point to incipient attacks as they commence. Unless attackers are savvy enough to erase log files (and alas are), firewall logs can also help you document successful or attempted attacks after the fact. Most boundary devices, which include not only firewalls but also screening routers, application gateways, proxy servers, and so forth—and indeed should—various kinds of activity routinely. Given that such logs can be very important sources of evidence in cases where strong evidence is needed, most devices log a wide range of traffic and various types of activity.

Because so many devices run in UNIX-based or UNIX-like environments, the good news is that the same information covered in the preceding section about the Syslog facility and generic Linux or UNIX logging techniques often applies to firewalls, routers, and other devices. For example, Cisco devices run a Cisco proprietary operating system, known as the Internet Operating System or IOS, this software uses a reasonably standard Syslog implementation to support its logging capabilities. With the proviso in mind that low-level details vary from system to implementation to implementation, our general coverage of logging facilities and operation remains applicable to many (if not most) boundary devices in wide use.

Add-software products that can monitor and analyze firewall logs are available. For example, firelogd is a daemon that monitors Linux firewall logs. Fwanalog is a script that parses and summarizes firewall log files on UNIX and Linux systems. Stonylake Firewall Reporter is a server application that runs on Windows and Linux, and provides more than 150 reports to help in data analysis. ZoneLogAnalyzer imports the logs from ZoneAlarm firewalls into an easily queried database. Web Trends makes a Firewall Suite that processes log files from Check Point, Cisco, Microsoft ISA Server firewalls, and others.

Logging is only one of the ways in which firewalls and other boundary devices can provide information about the activity and traffic they track. Firewalls (and other boundary devices) do indeed create log files, where all kinds of data may be written and stored for the long term. But these devices also support various types of other outputs, some of which can be important:

- Alarms: These systems can be instructed to issue high-priority messages in various formats should particularly suspicious activities or events occur. Many such systems can send e-mail messages to specific respondents and even page designated telephone numbers, in addition to logging information when specified events occur. This functionality permits systems to provide immediate responses from responsible individuals. Because routers, firewalls, and other boundary devices may be subjected to ping floods or other denial-of-service (DoS) attacks, and because they may witness failed login attempts that likewise signal that attacks have commenced, immediate action is essential in responding to such events.

- Alerts: Some types of traffic activity are less obviously symptomatic of attack but should be looked into nonetheless. This explains why many boundary systems can also issue alerts when particular conditions occur. Although these alerts may also result in e-mail or pager calls, they are usually less urgent than outright alarms.

- Reports: Although reportable events fall into the more mundane category of cataloging and categorizing traffic, activity, errors, and failed log or other access attempts, most boundary devices can also report aggregate behavior and statistics over some specific period of time (daily, weekly, monthly, and so forth). Such reports are important indicators of overall system health and security should be consulted regularly as part of the system monitoring and maintenance process.

In fact, most operating systems have some kind of alarm or alert facility as well. For example, Windows NT, 2000, XP, Server 2003, and Server 2008 support system alerts to administrators of system performance- or error. When it comes to what kind of information occurs in a firewall log, it usually consists of simple text records that document various aspects of network traffic. Though here again the details will vary to some extent, no log record is complete without including at least the following (and usually more than appears in this brief list of common log entry fields):

- Timestamp: Date and time at which the event, activity, or communication occurred
- Source address: Reported IP address for traffic source
- Source domain name (if available): Reported domain name for traffic source
- Destination address: Target delivery address for service in use
- Protocol: Name of IP protocol or service in use
- Message type or class (where applicable): Type of message being sent
- Port address (where applicable): TCP or UDP port to which the message is directed
- Socket address (where applicable): Socket address to which the message is directed

In some cases, log entries also include what's called a reverse DNS lookup or a backtrack. You can configure some boundary devices to double-check the official IP address associated with domain names reported for inbound traffic against the actual IP address included in incoming traffic. When these two values differ, it can be a definite indicator of spoofing, which in turn may mean suspicious activity (if not an outright attack) has ensued. This type of detection usually triggers an alert or alarm for reason.

Earlier, we mentioned that firewalls and other simple boundary devices lack some degree of intelligence when it comes to observing, recognizing, and identifying attack signatures that may be present in the traffic they monitor and the log files they collect. Without sounding critical of such systems' capabilities, this deficiency explains why intrusion detection systems (often abbreviated as IDSes) are becoming increasingly important in helping to maintain proper network security.

# Commercial Intrusion Detection Systems
