
## Chapter 21 Network Management and Debugging

IF-MIB::ifInOctets.1 = Counter32: 2605613514
IF-MIB::ifInOctets.2 = Counter32: 1543105654
IF-MIB::ifInOctets.3 = Counter32: 463123455
IF-MIB::ifInUcastPkts.1 = Counter32: 3895361556
IF-MIB::ifInUcastPkts.2 = Counter32: 8929592655
IF-MIB::ifInUcastPkts.3 = Counter32: 77123235

In this example, we see some general information about the system, followed by statistics about the host's network interfaces: lo0, eth0, and eth1. Depending on the MIBs supported by the agent you are managing, a complete dump can run to hundreds of lines.

## SNMP data collection and graphing

Network-related data is best appreciated in visual and historical context. It is important to have some way to track and graph performance metrics, but your exact choice of software for doing this is not critical.

One of the most popular early SNMP polling and graphing packages is MRTG, written by Tobi Oetiker. MRTG mostly written in Perl, runs regularly out of **cron**, and can collect data from any SNMP service. Each time the program runs, new data is stored and new images are created.

Another useful tool in this area is RRDTool, also by Tobi Oetiker. It is an application tool for storing and graphing performance metrics. All leading open source monitoring solutions are based on RRDTool, including our favorite, Cacti. Cacti, available from cacti.net, offers several attractive features. Using RRDTool as its back end, it monitors data in zero-maintenance, statically sized databases. Cacti stores only enough data to create the graphs you want. For example, Cacti could store one sample every minute for a day, one sample every week for a year. This consolidation scheme lets you maintain important historical information without having to store unimportant details or consume your time with database administration.

Second, cacti can record and graph any SNMP variable, as well as many other performance metrics. You're free to collect whatever data you want. Combined with the NET-SNMP agent, cacti generates a historical perspective on any system or network resource.

Exhibit D shows some examples of the graphs created by Cacti. These graphs show the load average on a server over a period of weeks along with a day's traffic on a network interface.

Cacti sports easy web-based configuration as well as all the other built-in benefits of RRDTool, at rrdtool.org for links to the current versions of RRDTool and Cacti, as well as dozens of other monitoring tools.

## Exhibit D Examples of Cacti graphs

![](img/579efec8c67772f31ecf34844bbb71a2_935_0.png)

![](img/579efec8c67772f31ecf34844bbb71a2_935_1.png)

## Nagios: event-based service monitoring

Nagios specializes in real-time reporting of error conditions. It includes scores of scripts for monitoring services of all shapes and sizes, along with extensive SNMP monitoring capabilities. Perhaps its greatest strength is in its modular, highly customizable configuration system that allows custom scripts to be written for any conceivable metric. Although Nagios does not help you determine how your bandwidth has increased over the last month, it can page you when your web server goes down.

The Nagios distribution includes plug-ins that supervise a variety of common points of failure. You can wrap up new monitors in Perl, or even in C if you are feeling ambitious. For notification methods, the distribution can send email, generate web reports, and use a dial-up modem to page you. As with the monitoring plug-ins, it's easy to roll your own.

In addition to real-time notifications of service outages, Nagios keeps a historical archive of this data. It provides several powerful reporting interfaces that track availability and performance trends. Many organizations use Nagios to measure compliance with service level agreements; Exhibit E on the next page shows the availability of a DNS server.

## Exhibit E Server availability as shown by Nagios

![](img/579efec8c67772f31ecf34844bbb71a2_936_0.png)

State Breakdowns:

Nagios works very well for networks of fewer than a thousand hosts and devices. It is easy to customize, and it includes powerful features such as redundancy, remote monitoring, and escalation of notifications. If you cannot afford a commercial network management tool, you should strongly consider Nagios. You can read more at nagios.org.

## The ultimate network monitoring package: still searching

As we reviewed the state of network management packages for this edition of the book, we found the software landscape bustling with activity, just as it has been for most of the last decade. However, most packages are still using RRDTool where in it gets to do their logging and graphing. No high-level standard akin to vi or emacs has yet arrived on the scene.

Two well-funded companies based on the "open source plus" model (GroundWork Open Source and Zennos) have debuted network management packages backed by serious advertising and polished interfaces. In the traditional free software area, the packages Munin (munin.projects.linpro.no) and collectd (collectd.org) have gained quite a following.

Munin is very popular in the Scandinavian countries. It's built on a clear architecture in which the data collection plug-ins not only provide data but also tell the system how the data should be presented.

collectd is written in C for performance and portability. It can run on even tiny systems without hampering performance or requiring any additional dependencies. At the time of this writing, collectd comes with over 70 data collection plug-ins.

## Commercial management platforms

Hundreds of companies sell network management software, and new competitors enter the market every week. Instead of recommending the hottest products of the moment (which may no longer exist by the time this book is printed), we identify the features you should look for in a network management system.

**Data-gathering flexibility:** Management tools must be able to collect data from sources other than SNMP. Many packages include ways to gather data from almost any network service. For example, some packages can make SQL database queries, DNS records, and connect to web servers.

**User interface quality:** Expensive systems often offer a custom GUI or a web interface. Most well-marked packages today tout their ability to understand XML templates for data presentation. A UI is not just more marketing hype—you need an interface that relays information clearly, simply, and comprehensibly.

**Value:** Some management packages come at a stiff price. HP's OpenView is both expensive and one of the most widely adopted network management systems. Many corporations define value in being able to say that their site is managed by a high-end commercial system. If that's not important to your organization, you should look at the other end of the spectrum for free tools Cacti and Nagios.

**Automated discovery:** Many systems offer the ability to “discover” your network. Through a combination of broadcast pings, SNMP requests, ARP table lookups, and DNS queries, they identify all your local hosts and all the discovery implementations we have seen work pretty well, but none are very accurate on a complex (heavily firewalled) network.

**Reporting features:** Many products can send alert, activate agents, and automatically generate tickets for popular trouble-tracking systems. Make sure that the platform you accommodates flexible reporting; who knows what devices you will be dealing with in a few years?

**Configuration management:** Some solutions step far beyond monitoring and alerting. They enable you to manage actual host and device configurations. For example, a CiscoWorks interface allows you to change a router’s configuration in addition to monitoring its state with SNMP. Because device configuration information deepens the analysis of network problems, we predict that many packages will develop along these lines in the future.
