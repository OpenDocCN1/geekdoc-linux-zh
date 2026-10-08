
## EMS requires monitor requests to be initiated on each local node

EMS requires monitor requests to be initiated on each local node; however, this also allows monitor requests to be customized to the local systems so that only the critical resources need to be monitored. EMS should not be considered an enterprise framework because it lacks the ability to enable monitoring across multiple systems easily.

Using the EMS GUI to configure each resource instance to be monitored may be time-consuming. The EMS Configuration GUI supports some wildcarding to make the configuration easier. Also, the EMS Hardware Monitors available with Online Diagnostics come preconfigured. If you are using IT/O, a tool called monvols is available to help you configure all the logical or physical volumes for a selected system. The monvols tool and other tools and templates for EMS are available for free when downloading the EMS Developer's Kit from the Web at http://www.software.hp.com/products/EMS. Note, however, that monvols is available only for HP-UX 10.20.

To configure most EMS monitors, you use SAM. From its Resource Management functional area, you can select the Event Monitoring Service to launch the EMS GUI, and then add a new monitoring request. The initial configuration screen is shown in Figure 3-4.

### Figure 3-4 Initial EMS configuration screen

![](img/eae88b61ada165139a1d9b546a34140b_45_0.png)

MC/ServiceGuard provides one GUI, as well as command-line and configuration-file options, to configure packages to be dependent on EMS resources. In this case, event notification is sent directly from a resource monitor to MC/ServiceGuard.

The EMS configuration tools enable a user to configure a resource or set of resources to be monitored. The user chooses the type of notification desired based on applications available in the customer environment. For example, if events should be sent to an OpenView management station, the user can choose SNMP notification. SNMP can also be used to send events to other management stations, such as IBM NetView, Tivoli, or CA Unicenter TNG. If IT/O is being used, opcmsg notification is available on IT/O managed nodes. Although EMS is often used with a management platform such as HP OpenView, HP OpenView is not required. For example, if a customer has written a custom fault-recovery application, event notification could be received directly by the application, using TCP or UDP.

The EMS configuration tools also enable you to browse the list of resources that can be monitored dynamically. This allows a resource monitor to monitor different resource instances on different systems, and provides a standard interface for operators to find available monitors. You can then customize the monitoring for each system. Although EMS provides more flexibility, it is also more difficult to configure, because configuration is generally done once per system.

First, the operator browses through the available resources. Then, he or she selects a resource to monitor and specifies the monitoring parameters, such as thresholds and polling intervals. After the monitor request is made, the operator is returned to the main EMS screen, where all active EMS monitor requests are displayed.

EMS hardware monitor configuration is done by using the Hardware Monitoring Request Manager, monconfig. Notification conditions can be configured in a consistent way for all the supported hardware resources on the system. As hardware is added to the system, monitoring can be enabled automatically and consistently with the way similar hardware is being monitored.

If requesting SNMP trap or opcmsg notification, additional configuration is usually required on the management station. EMS provides templates that can be used in OpenView NNM or IT/O to recognize and format traps and opcmsg notifications for viewing in their respective event browsers.

## Monitor Developer's Kit

EMS provides a Developer's Kit to make it easy for customers and third parties to integrate or write their own EMS monitor programs. Customers can define their own important resources to be monitored. Using the EMS Developer's Kit also ensures that monitors will behave in a standard way.

The EMS Developer's Kit includes the necessary header files and libraries to write a custom resource monitor. Monitoring APIs are provided for the monitor to receive requests, wait during polling intervals, and send notifications. A sample monitor is also provided. The mechanism to actually check the value of a resource is resource-dependent, but APIs are provided to determine whether notification should be sent based on the value of a resource. The monitor provider does not need to write code to send different types of notification, such as SNMP traps or e-mail; this is handled by the EMS framework.

All the products in this chapter provide some mechanism to allow you to add your own resource monitors. EMS monitors are more difficult to develop because they require you to write a program instead of merely writing some scripts. EMS, however, provides more flexibility, because its monitors do not have to rely on HP-UX commands to gather data.

Information on using the EMS Developer's Kit is included with other software that is downloadable from the HP software Web site. You can find the Developer's Kit along with HP OpenView templates and other tools at http://www.software.hp.com, under the High Availability Software product category. EMS manuals are available at http://docs.hp.com/hpux/ha.

## Notification Methods

EMS was designed specifically to support monitors for high availability resources. Consequently, it supports notification by using an HP-proprietary interface to MC/ServiceGuard. However, EMS can be used without MC/ServiceGuard and it supports an unusually large variety of notification options, including:

- SNMP traps
- IT/O's RPC mechanism (opcmsg)
- E-mail
- Logging to the system log file, the console, or a specific log file
- UDP or TCP messages

Notification is sent on a per-request basis, which provides additional flexibility. Several EMS events can be managed concurrently, as shown in this example:

- Client A requests Event 1 via SNMP
- Client A requests Event 2 via opcmsg
- Client B requests Event 1 via TCP
- Client B requests Event 3 via TCP
- Client C requests Event 3 via opcmsg

Notification is then sent to the specified clients when the events occur.

## Diagnostic Capabilities

EMS enables the monitor to provide arbitrary data, up to 10,000 bytes, along with an event notification. This information can be unique for each event notification and it can contain vital diagnostic information. For example, a disk failure event could include the serial number of the failed disk device in its monitored data area. Additional text could describe how to fix a failed component. Monitor providers taking advantage of this capability must document how operators should interpret this information.

EMS Hardware Monitors provide detailed information about the cause of an event and give recommended actions.

Unlike other products, such as Unicenter TNG, EMS doesn't provide the ability to take automated actions in response to events. However, you can have events sent to your own customized fault-recovery application by configuring the TCP or UDP notification methods. If EMS is used with IT/O, then you can also configure templates and recovery actions into IT/O.

## Additional Information

The EMS framework is freely available from HP with the Online Diagnostics on the support media and the application CD-ROMs.

For the latest information on EMS, check the HP High Availability Web site at http://www.datacentersolutions.hp.com/2_3_index.html. The EMS manuals and release notes are available at http://docs.hp.com, under High Availability.

You can learn more about the Hewlett-Packard diagnostic tools, including the EMS Hardware Monitors, on the Web at http://docs.hp.com/hpux/systems.

## PLATINUM ProVision

PLATINUM technology, Inc. has a suite of products called ProVision (originally Enterprise Performance Management). The ProVision product suite collects server, database, and network performance information and has four components: DBVision, ServerVision, WireTap, and TransTracker. Data can be collected by agents running either locally on the managed system or remotely over the network. All of these components, except for TransTracker, share the same ProVision console, an NT or X Windows GUI.

ProVision has agents collecting performance data, which then is stored in a database. Configuration parameters determine when to archive, delete, and compress data. These parameters can vary for each individual metric. Utility programs are available to export and import archived data.

PLATINUM also provides solutions for software distribution and remote execution (AutoXfer), problem resolution (Apriori), security (AutoSecure), data warehousing, disaster recovery, and capacity planning.

The PLATINUM tools are accessed through an interface called PLATINUM Director, which provides monitoring through different user-configurable perspectives. Operators can use either a graphical view, showing the status of system resources or applications, or a Windows Explorer-like view, showing systems listed in a hierarchical tree format. From a Director console, administrators can first see a high-level view of events and system status, and then drill down to take actions. The Alarm window shows the status and descriptions of events, with event-specific actions available from a pull-down menu.

From the Director Explorer view, the administrator can select a system and then launch other tools, such as the job scheduler, to view the job status for a system. The AutoXfer tool can be launched to distribute software.

AutoSecure and AutoSys are certified with MC/ServiceGuard. AutoSys and Apriori have been integrated with HP OpenView. A much more complete integration has been done with Tivoli TME.

### Monitored Components

DBVision is PLATINUM’s product for database monitoring. DBVision gathers database statistics and supports Oracle, Sybase, Informix, and DB2. Events such as resource thresholds can be sent from different databases to a central console, where corrective actions can be taken. DBVision can detect problems such as running out of available tablespace, processes waiting for locks, and runaway processes.
