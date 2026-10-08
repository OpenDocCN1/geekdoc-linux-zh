# Monitor Discovery and Configuration

You need to install the PATROL agent and KMs on each system to be monitored. Once this software is installed, you need to load (or activate) the KMs you intend to use on each system. This can be done from PATROL’s operator console.

PATROL agents discover all databases, applications, and key resources when they are started. This makes it easy to start monitoring quickly. The administrator can also define additional applications and databases so that they can be discovered in the future.

Figure 3-5 shows an example of the resources being monitored by PATROL on a system called “bakers.” This system has the KMs for UNIX and for Oracle loaded. You can drill down on each of these resource’s classes to see the metrics being monitored, graph data, and check status.

In addition to monitoring, PATROL can automate recovery actions taken in response to error or failure conditions. The user must assign the desired recovery actions to an event. The concept of operator-initiated actions, available with IT/O, is not supported with PATROL.

PATROL can be configured to respond automatically to specific problems, and can help tune databases for optimal performance. Recovery actions can be performed locally by agents without requiring communication with the console.

Users can set thresholds. Events are sent by the PATROL Event Manager to the PATROL console. All metrics are sampled simultaneously, which can cause unnecessary system overhead for resources that are less critical or that rarely change.

# Monitor Developer’s Kit

BMC PATROL has an API that enables events to be sent by a non-PATROL program to the PATROL Event Manager. This is similar to IT/O, which has an API for sending RPC messages to its Event Browser. A non-PATROL program can also receive events from PATROL.

The PATROL Scripting Language (PSL), part of the PATROL Developer Console, can be used to create scripts to perform recovery actions by the PATROL agent on managed nodes. PSL can also be used to write parameters, commands, tasks, and discovery procedures for PATROL agents.

# Notification Methods

PATROL Alarm Manager can be used to send notifications by pager, by e-mail, or to third-party messaging systems. Users define the resources to monitor and the notification criteria. After configuration, the alarm policies can be distributed to a predefined set of systems. The PATROL Alarm Manager keeps track of additional information, such as the number of events sent by a host, and time periods during which notifications should be sent. PATROL can also send copies of an event to multiple consoles.

The PATROL Event Translator (PET) can translate messages for various protocols. BMC provides a PET for IT/O, using the OpenView APIs, but it forwards only the event. The operator must switch to the BMC PATROL console to initiate corrective actions.