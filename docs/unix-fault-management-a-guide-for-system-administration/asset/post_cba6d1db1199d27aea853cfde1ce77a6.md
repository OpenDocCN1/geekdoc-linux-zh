
These MIBs provide information that can help with configuration management, resource management, and fault management. For performance management, I/O rates can be calculated by monitoring performance metrics in the RDBMS MIB. Collecting I/O rates over time can provide with a simple way to track I/O performance.

Although access to MIB data is readily available, MIB browsing is a manual process, usually requiring you to poll for the information you need. The manual query captures only a snapshot. Like many metrics, you really need to collect the information over a period of time, so that you can make comparisons.

## Database Vendor Tools

This section describes some monitoring capabilities provided by the database vendors. Later sections discuss the sophisticated database monitoring tools provided by third parties.

## Oracle Enterprise Manager

Oracle has developed a database management platform called the Oracle Enterprise Manager (OEM) for database administration. OEM includes utilities for monitoring network and database objects, scheduling jobs on multiple systems, and distributing software. Oracle Diagnostics Pack, Oracle Tuning Pack, and Oracle Change Management Pack are optional software packages that provide additional capabilities, such as database tuning and capacity planning. OEM has many different components, including the following:

- **Console**: Includes functions for mapping and event management. Navigator windows show hierarchies of objects, such as listeners, names servers, and databases, which you can select and show on maps. You can use filtering to reduce the number of objects shown. You can create Map windows to show only the important objects that you need to monitor, by dragging objects from the Navigator hierarchy into the Map window. After you create and customize maps, you can save and recall them at any time via menu options. The console can also be used to monitor active jobs and job history. An Event window shows events occurring on databases, listeners, and nodes. You can acknowledge events or see a history of events, which includes the name administrator that acknowledged the event.
- **Repository**: A set of database tables that is used to store information about the tasks associated with a given administrator and any customized views that have been defined. The repository database can be on any node accessible to the OEM console. To use OEM, you connect or log in to the console, which then finds the repository associated with your user name.
- **Intelligent agents**: Processes running on remote nodes in the network. To monitor events on a remote server or to schedule and run remote jobs, an intelligent agent must be running on that server. The intelligent agents can detect when a configured event has occurred. When an agent detects an event, it can automatically launch recovery actions and send notification to administrators.
- **Communication daemon**: Used by the console to communicate with the intelligent agents. Events are sent by the agents to the console. When received at the console, the events appear in the Event window. If you are not currently logged in, events are queued until the next time you log in to the console.

The database objects need to be registered at the console to maintain their status. Status is shown graphically, with color indicating severity. Objects can be grouped together with a special container icon. The worst status of any of the members is propagated to the group icon. Hierarchies of groups can be created, and you can take actions on a group.

Objects also have property sheets. The database property sheet can show status, or it can be used to start or stop a database. Database administration tools shown in the Tools Application menu can be launched on an object by first selecting the object and then selecting the tool. The OEM database administration tools can be used to manage schema objects, back up, recover, and restore a database, and distribute software.

The events shown in the Event window contain a variety of information, including the name of the event, event severity, source node, type of event, and timestamp. Event severities are shown with different colors. Events also affect the color of the object in the Map window. Threshold parameters determine whether the event should be displayed as a serious alert or merely as a warning. Events can be acknowledged and then annotations can be associated with an event.

OEM contains a predefined set of events that can report the status of nodes, databases, and listeners. You choose the events and then set the polling interval and threshold conditions that determine when the events should be generated. You do this from the Event menu at the OEM console. After you create an event set, you need to register it, to be able to monitor events on a specific system. During registration, you specify who to notify and how notification should be sent. To allow for different administrators to receive different events based on their responsibilities, each administrator’s mail address or pager number, system responsibility, and availability need to be configured. E-mail and paging are two notification options. Notification can also be sent directly to the console or forwarded to SNMP-based management stations.

OEM is also extensible. You can write your own applications that can be launched from the console. A scripting capability can be used to create customized events.

Jobs are run by intelligent agents on the local system, so connectivity with the OEM console is needed only when a job is initially scheduled. If the agent is unavailable, the job request is queued until the agent becomes available. Jobs can be scheduled to run on a set of databases or nodes, or on a user-defined group of objects.

Recovery actions can be configured to run as jobs when an event occurs. These are referred to as “fixit” jobs. The Job Scheduler can be used to create these jobs. This type of job runs as a recovery action in response to an event, instead of being scheduled for execution, which is the Job Scheduler’s usual task. The job is submitted to an agent at the remote node where the event is being monitored. The job, for example, may execute a predefined SQL*Plus script file or a UNIX command or custom script that you created.

The previously mentioned predefined fault management events that come with OEM provide status information on the database, listener, and computer system. Predefined resource and performance management events require the additional purchase of the Oracle Diagnostics Pack, which includes the following Oracle components:

- **Performance Manager**: Used to collect system and database performance information and display the data in charts or graphs on the OEM console. The user can control the sampling interval. The available data includes CPU utilization, library and dictionary cache performance, and memory sort performance.
- **Capacity Planner**: Used to analyze system and database capacity information. You can use this information to plan for future growth.
- **Trace Manager**: Used to start and stop data collection for applications that use the Oracle Trace API (described later in this chapter). Using the Trace API, the Trace Manager can discover all the applications that are on systems managed by the console.
- **Trace Data Viewer**: Enables you to examine the information from the data collections from the Trace Manager.
- **TopSessions**: Used to identify the database sessions that are using the most system or database resources. The list can be based on resource usage, open cursors, user transactions, or block changes. Runaway sessions can be identified and then terminated.
- **Advanced Events**: Provides additional sets of predefined events to be used with the OEM, such as additional fault management events, and resource and performance-management events.
- **Lock Manager**: Used to graphically monitor the use of database locks. You can also see who is waiting for or using individual locks.

All events discovered by the OEM agent can also be sent as SNMP traps (defined in Oracle's OEM MIB). The following is a list of the events that can be sent as SNMP traps from the OEM agent:

- Unknown event
- Database has gone down
- Database has new message in its alert log
- OEM unable to establish a new connection to database
- Process blocked on lock held by a user session
- Database archive log full
- Database dump device full
- Tablespace segment approaching maximum extent
- Tablespace segment unable to allocate additional extents
- Number of database data files approaching maximum allowed
- Current database locks approaching maximum allowed
- Current database processes approaching maximum allowed
