
In addition to determining what has gone wrong, you may want to take corrective actions. With some products, these actions can be predefined and automatically taken when an event arrives. In some cases, the actions are available, but need to be executed by the operator. You also need to be able to easily record the results of any actions that were taken, to help track the status of problem resolution.

## IT/Operations

IT/Operations (IT/O) is an HP OpenView application that provides central operations and problem management. IT/O is a software bundle that not only includes NNM for network management, but also provides capabilities in the area of system management. With IT/O, facilities are provided that enable operators to share the management station software, and also have individual responsibilities for different sets of managed systems or types of events.

IT/O uses intelligent agents that run on each managed system to monitor and collect management information, messages, and alerts, and to send the information to a centralized console. The agents can also perform local actions without communicating with the management station. After receiving events, IT/O can initiate automatic corrective actions or prompt the operator to run predefined, operator-initiated actions. When an operator reads an individual message, guidance is given and actions may be suggested for further problem resolution or recovery.

IT/O has four main windows:

- **Node Bank:** Displays the systems managed by the operator as icons, and allows organization of the icons into node groups, which then can be viewed from the Node Group window.
- **Message Groups:** Displays logical message groups, such as Performance, Oracle, and Backup. The message groups serve as one way to organize messages in the Message Browser window.
- **Message Browser:** Shows the events that have been received by the management server, including instructions, annotations, results of automatic actions, performed actions, and acknowledgments.
- **Application Bank:** Provides access to commonly used diagnostic and administrative applications.

These four main IT/O windows are shown in Figure 3-1.

The Message Browser can filter out messages from systems that you don't care about. If you are responsible for only a specific system function, such as performance, you can configure the Message Browser to show only those messages from a specific message group.

## Monitored Components

As previously described, IT/O provides assistance with multiple aspects of system monitoring, especially faults, and resource and performance management. IT/O can also help with security monitoring, with its predefined template for monitoring root login attempts.

**Figure 3.1 IT/O main windows.**

![](img/eae88b61ada165139a1d9b546a34140b_34_0.png)

IT/O comes with predefined monitors and templates. Templates are used to configure monitors, to define message conditions, and to match patterns on received events. Templates also define Event Browser message text, severity levels, message groups, instructions, and actions. Monitors are predefined for e-mail, CPU utilization, swap utilization, and filestem utilization, among other things. Log file templates monitor system log files for system errors, su (switch user) events, logins, logouts, and kernel messages. Templates and message conditions can be modified so that the operator gets paged under certain conditions.

Many other tools plug into IT/O to provide additional monitoring and management capabilities. IT/O has add-on modules for the managed node, called SMART Plug-Ins (SPIs). These modules provide customized knowledge of databases and applications via templates and monitors. For example, SPIs are available for SAP R/3, Baan, Oracle, and Informix. ClusterView is an HP OpenView application that provides monitoring of high availability clusters. Combined with the ability to do network and system monitoring, IT/O can provide a consistent interface for monitoring all of your components.

IT/O provides multiplatform support. The IT/O console is available on HP-UX and Sun platforms. IT/O can manage HP-UX, Sun Solaris, IBM AIX, and other platforms, including Windows NT.

## Monitoring Features

Each system being monitored must have IT/O managed node software installed on it. This software includes IT/O's intelligent agents, which monitor and collect data, perform actions, and send messages to the IT/O management console.

Managed nodes are displayed in the Node Bank window. System status is reflected by the colors of the node icons in the Node Bank. Propagation rules are configurable in IT/O. For example, the color of the node icons may represent the criticality of the most serious unacknowledged event in the Message Browser.

The IT/O agent is a key to differentiating the IT/O product. The agent is considered to be intelligent and autonomous because it can take actions without requiring operator intervention. The IT/O agent performs local polling of the resources being monitored, and can filter out redundant or unnecessary events before forwarding them to the management station. This can eliminate some network traffic and help to avoid information overload for the operator. The agent can also do event correlation, which further reduces network traffic. New events can be created by consolidating data from multiple events. The IT/O correlation engine can also reach conclusions based on the absence of events.

The IT/O agent can continue monitoring and taking automated actions autonomously if it loses its connection to the management station. The agent will store events so that when the management station comes back up, no events are lost. The agent also uses a secure and reliable Remote Procedure Call (RPC) mechanism, opcmsg, to communicate with the management station.

IT/O is useful when an operator needs to manage numerous systems consistently. Templates can be modified and then downloaded to a set of systems, enabling the operator to monitor many systems identically. In other words, monitoring can be set up in a consistent way for all systems.

IT/O receives inbound events (such as SNMP traps), performs filtering, and delivers events to other processes registered for notification.

Events received by IT/O are stored in a central repository, providing a permanent history and allowing for future analysis and auditing. Events are ordered chronologically and marked by severity. The name of the system that sent the message and a timestamp are stored with each event. Additional information includes the type of the event and application sending the event. When automated actions are provided, an indication is given as to whether an action was successful. Annotations can be used to show the output from the actions.

Filtering can be used on the management station to reduce the number of events visible in the Message Browser. Filters can be based on severity, originating system, message group, or other categories.

Events in the Message Browser may be the result of an SNMP trap, log file monitoring done by an IT/O agent, or an opcmsg call made by an IT/O monitor application. Events may indicate faults, status changes, configuration changes, performance thresholds being exceeded, and so forth. Events are kept in the Message Browser until they have been acknowledged. Events can also be forwarded to other management stations or to trouble-ticketing systems.

IT/O enables you to assign roles to operators so that each can be responsible for different events, nodes, message groups, or applications.

It is important to be able to ensure that any monitoring you enable remains enabled. You don't want to lose critical events. Because the IT/O agent is responsible for obtaining the monitor data periodically, you need to ensure that the agent is always running, which you can do by using IT/O's capability of monitoring arbitrary processes. The agent can also be automatically restarted.

## Monitor Discovery and Configuration

After the intelligent, autonomous agents are installed, they monitor resources according to the templates that have been assigned to the local system. IT/O comes with a set of templates that are used to define monitoring conditions, thresholds, and event messages. The templates can include configured actions, either automatic or operator-initiated. This is where you may want to configure an action such as paging.

The Message Template window shows the message templates currently configured in IT/O. Templates are grouped. For example, a template group exists for HP-UX 10.x systems.

From the Node Bank window, you can assign templates to your managed nodes or node groups. After you assign all the templates, you need to install or update the IT/O software and configuration on the managed nodes. This can be done on one or more managed nodes, so that you can quickly set up monitoring for multiple systems. With IT/O, the templates are pushed out to each managed node so that the IT/O agent can then monitor, filter information, forward messages, and perform local actions without requiring communication with the management station.

Message templates are available for receiving SNMP traps. Message conditions are defined to specify which messages are displayed in the Message Browser, the format of the displayed messages, and any actions that should be performed when an SNMP trap matches a defined message condition.

A message group can be specified in a template. When message conditions are matched, the event gets assigned to the configured message group. This can be useful when delegating operator responsibilities. When configuring operators, both node group and message group responsibilities are assigned. For example, you can assign all HA (MC/ServiceGuard) messages to the operator responsible for monitoring MC/ServiceGuard clusters.

When configuring monitoring, you can also include instructions in the template or configure actions to be performed, either automatically or manually triggered by the operator.

As shown in Figure 3-2, you can assign templates from the Message Source Templates window to nodes in the Node Bank to configure monitoring and event management.

## Monitor Developer's Kit

IT/O provides default monitors for CPU utilization, disk space, and other resources. IT/O also allows users to create their own monitor scripts. The script-based monitors rely on the IT/O agent to poll them for information, but the agent can then send notifications on their behalf.
