
## Distinguishing Monitoring Frameworks

Customers are recognizing the need for management tools, and enterprise management framework providers — such as Hewlett-Packard, with its IT/Operations (IT/O), and Computer Associates, with its Unicenter TNG — are feeling pressured to provide low-cost alternatives. Both HP and CA have announced intentions to bundle low-cost versions of their software with HP-UX servers. Enterprise SyMON is a low-cost management station available on Sun systems, but because it currently lacks a developer’s kit, it is not a true monitoring framework.

According to a recent Network Computing Review of enterprise frameworks, the products “...are as complex as the problems they are meant to solve.” Monitoring frameworks can be difficult to set up and are very expensive, but the benefit is that you can monitor heterogeneous components and systems through a common interface.

This chapter describes some of the frameworks available for UNIX fault management. It identifies some of the monitoring capabilities provided or available with each framework. Hopefully, these descriptions will help you to determine which framework, if any, is best for your environment.

You may need to use multiple monitoring frameworks in your environment. Chapter 9 briefly describes how to integrate different combinations of these tools.

We have selected a variety of frameworks to discuss in this chapter. Each has different strengths and weaknesses. Describing all the available products would be difficult, but this chapter should give you insight into the capabilities you should expect from any product that you choose to evaluate. This chapter is meant to give you a very high-level overview of features; later chapters go into more detail on product differences.

For each product, we describe its breadth of monitored components, general monitoring features and capabilities, ease of setup, approach to extensibility (developer’s kits), notification flexibility, and diagnostic capability. These attributes are generally described in this opening section.

## Monitored Components

Each product’s breadth of coverage is described in this chapter. You should ensure that all the components that you need to monitor are available before you select a framework. Some products, such as CA’s Unicenter TNG, have a smaller set of metrics available than other products, such as BMC PATROL with its set of Knowledge Modules (KMs).

## Monitoring Features

This section on monitoring features describes the framework’s general monitoring capabilities, making special note of any unusual capabilities, such as IT/O’s event-correlation capability.

## Monitor Discovery and Configuration

The first step toward actually using a monitoring framework is to determine its set of available resource monitors. The methods of doing this vary depending on the framework being used.

You can obtain resource monitors in a variety of ways. Some are freely available when you purchase a computer, while others are included with the enterprise framework. Monitors can also be sold as add-ons to the framework. Another possibility is that the monitor for a product is included with the product itself. For example, Hewlett-Packard includes Event Monitoring Service monitors with many of its networking products.

Different frameworks have different approaches to help you find the available metrics and components to monitor. With MeasureWare, you use HP’s online help facility to explore the available metrics. Other tools provide a GUI to select the monitors to install or use.

After determining the available monitors, you need to choose and configure the ones that you want to use. Some monitors are configured automatically when they are installed, while others require that you manually define notification criteria and other information before they can be used.

### Monitor Developer’s Kits

The advantage of a framework is having all of your resources monitored through a consistent interface. However, a framework is unlikely to account for everything that might be interesting to you, especially if you have your own custom applications. In this case, you need an easy way to create a custom monitor that can be used seamlessly with the rest of the framework.

A defining characteristic of frameworks is that they provide some method to allow the customer to add a monitor, but these methods vary. Some enable you to add a monitor with scripts, while others require more programming.

### Notification Methods

To make administration easier, you should have all events sent to a common location. This may be a consolidated console or system log file, for example. Monitoring multiple systems from a master console reduces the need for additional hardware dedicated to monitoring. Sending messages to a single location makes diagnosis faster and less error-prone, because operators do not need to remember the names of key log files and do not need to remember to check individual logs.

The console or log file needs to be accessible anywhere. Of course, a system log file will be inaccessible if an event led to a system outage. Within a company, a system operator may need to access logs from a remote network. Network accessibility and security may be concerns when remote access is required.

Paging is an increasingly common technique for problem notification. According to a recent System Administrators Guild (SAGE, a USENIX technical group) study, a majority of administrators now carry pagers during nonworking hours. System operators may be paged at home to diagnose problems, so access from outside the company firewall may be an issue. Paging may require software that is not provided by the framework itself. Also, a terminal interface may be needed for remote access over a modem.

Ideally, the system operator has a management tool with a graphical representation of the network and systems, and an event log file. Without a consolidated console for the managed environment, the operator is forced to log on to the system, if accessible, and troubleshoot by using local log files. Many software products write error information to the system log file, /var/adm/syslog/syslog.log.

Notification can be as simple as a color change on a system's front panel display. Notification can also be much more sophisticated, such as an ASCII message appearing on the operator's console, with the color reflecting criticality, and with actions suggested or automatically taken to try to recover from the problem.

Industry-standard notification methods include Simple Network Management Protocol (SNMP) traps, and Desktop Management Interface (DMI) notifications. SNMP traps are commonly used on UNIX operating systems, including HP-UX, for event notification. Support for DMI has only recently been added to HP-UX.

Some tools, such as the Network Node Manager (NNM), discussed in Chapters 4 and 6, rely on SNMP traps or sent from the UNIX system to keep their network topology and maps up-to-date. They may also use SNMP to poll the systems periodically.

Many of the enterprise management frameworks provide SNMP trap handlers so that they can receive events as traps and log and display events in an event browser. Templates are needed on a management station to translate SNMP traps into an ASCII-readable format. A user can configure these templates. Some HP and third-party products provide respective OpenView templates.

Because SNMP uses an unreliable network protocol, some management frameworks provide an additional reliable mechanism. IT/O, for example, uses a proprietary Remote Procedure Call (RPC) mechanism called opcmsg. With opcmsg, you can be assured of receiving notification.

In some cases, you may not want to be notified when an event occurs, because a recovery action may have already taken place. For example, when MC/ServiceGuard software detects that a Network Interface Card (NIC) has failed, it automatically configures a standby NIC, and network traffic transparently switches to the new interface. However, even in this simple example, you probably want to be notified, to ensure that the failed NIC is fixed in a timely manner.

Events can also be sent into event correlation engines, which can do some event processing and filtering on behalf of the operator. This is described in more detail in Chapter 9.

If you have a support contract, you may want to have your customer support center notified automatically when problems occur. HP Predictive Support software has the ability to send events via modem to the HP Response Center.

You need to determine whether or not the framework you want to use has a sufficient set of notification methods available.

## Diagnostic Capabilities

Another way to compare frameworks is by their diagnostic capabilities. For example, after you receive notice of a problem, how easy can you troubleshoot and resolve the problem with each of the frameworks? Some products, such as IT/O, can provide detailed instruction information along with every event.
