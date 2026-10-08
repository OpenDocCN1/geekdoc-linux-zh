IT/O can also be used to monitor specified components on a managed system. Some predefined monitors are provided, one of which has the ability to monitor specific processes. An event is sent to the IT/O console if a process fails. A recovery action can be configured to restart the application.

Although IT/O can detect an application failure and restart the application, it does not have sufficient high availability capabilities to move an application to another system or ensure that only one copy is running. More extensive high availability capabilities are provided by MC/ServiceGuard, which is discussed next.

# ## MC/ServiceGuard

MC/ServiceGuard is a high availability product from Hewlett-Packard that is used to protect your critical applications and servers. MC/ServiceGuard is most commonly used in a multisysem (cluster) environment. The MC/ServiceGuard software on each system monitors the other systems in the cluster. MC/ServiceGuard can detect the failure of systems, networks, and applications. For example, MC/ServiceGuard can recover transparently from a LAN failure.

After deciding which applications need to be protected, you configure them as packages by using MC/ServiceGuard commands or the graphical interface accessible from SAM. Numerous attributes of the application need to be defined, such as the following:

+   - Name of application
- Scripts used to start and stop application
- Processes or services that make up application
- Subnetworks used by application
- Alternate systems on which application can run
- Additional resource dependencies

MC/ServiceGuard then monitors these services and dependencies. If a failure occurs, the package is either restarted locally or moved and restarted on another system. Similarly, when a system failure occurs, MC/ServiceGuard software can detect the problem and automatically restart critical applications on an alternate node.

MC/ServiceGuard software detects a variety of error conditions, but does not have a sophisticated notification mechanism for you to learn what happened. Errors are often written to the system log file, which helps retrace what happened.

Because MC/ServiceGuard can automatically move applications to other systems, it may be difficult for you to know the current status of your application. MC/ServiceGuard commands, such as cmviewcl, can tell you the current state of a cluster and its packages. The HP MC/ServiceGuard MIB also contains this information. However, a package can be moved for a variety of reasons, and MC/ServiceGuard doesn't tell you the reason. You may want to check the system log file (\var\adm\syslog\syslog.log) on each cluster system for its specific MC/ServiceGuard activity. An example of the events logged to the system log file during a package failover