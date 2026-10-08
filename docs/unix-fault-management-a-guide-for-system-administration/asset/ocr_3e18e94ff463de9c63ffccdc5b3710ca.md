ECS also integrates with NNM. ECS can discover the network topology from NNM and can use it for correlation. It also comes with some out-of-the-box correlation circuits for network event correlation.

# Seagate NerveCenter

Seagate NerveCenter provides network event correlation and behavior management for UNIX and NT systems. It uses rules-based filtering and advanced correlation to pinpoint root causes and help you manage the volume of critical network issues and events in the enterprise. NerveCenter can also be configured to perform automated corrective actions.

NerveCenter has three main components: NCServer, AdminTool, and NC Client. The NCServer maintains a database of events. It detects events, distributes information to clients, and communicates with the network management platform. The AdminTool is used for maintaining and configuring NerveCenter domains.

NerveCenter comes with a graphical alarm interface. It provides a display to show the health of the environment at a glance. There is an Alarm and Traffic Summary window that shows existing alarms and their severity.

Rules are also user-configurable via a drag-and-drop GUI. The user can specify particular events and define corrective actions.

Behavior models are used to define the relationships between critical conditions and specific corrective actions. NerveCenter comes with several predefined models for monitoring network traffic, performance, status, security, and error conditions.

There are many different types of automatic actions available to configure for specific events. The following is a list of automatic actions available from NerveCenter:

+   - Send a notification to a management station or another NCServer.
- Execute a UNIX or NT command or Perl script.
- Log data to a file or database.
- Send a page or e-mail.
- Send an SNMP trap.
- Perform an SNMP set.

NerveCenter correlates across network devices, UNIX systems, and NT systems. Correlation can be done at a central management station or using a distributed management model. In the distributed model, each NCServer is responsible for managing different domains.

NerveCenter correlates events through SNMP polling and listening for SNMP traps. It can be configured to monitor specific MIB variables. New MIBs can easily be added, so NerveCenter can be configured to poll additional MIB objects.

NerveCenter integrates in most network management platforms, including OpenView NNM and IT/O, IBM NetView for AIX, Tivoli TME, and Unicenter TNG. It can also be run standalone. With IT/O integration, NerveCenter can forward messages to IT/O, and IT/O can forward messages to NerveCenter.