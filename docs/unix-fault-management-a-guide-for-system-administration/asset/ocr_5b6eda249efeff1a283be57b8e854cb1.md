The MC/LockManager product is modeled after MC/ServiceGuard and provides support for concurrent database access to Oracle databases by using Oracle Parallel Server. This cluster solution can provide continuous access to the database despite the loss of a server. MC/Lock-Manager relies on the generic monitoring capabilities of MC/ServiceGuard, and also monitors the Distributed Lock Manager.

MC/ServiceGuard provides help for database fault management only. It does not help you to manage database resources and performance, and provides no help for monitoring service response time to detect performance issues or uncover trends that could lead to problems.

Note that MC/ServiceGuard is supported only on HP 9000 Series 800 systems running HP-UX 10.x or later operating systems. Similar high availability cluster products are available for other platforms, such as Solstice HA for Sun Solaris environments.

# ## ClusterView

ClusterView is an HP OpenView application that can be used to monitor MC/ServiceGuard or MC/LockManager clusters. ClusterView presents windows for each high availability cluster in a company's environment. In each window, you can see the status of packages and the systems on which applications are running. ClusterView can show database servers and their status, if they are configured as MC/ServiceGuard packages.

# ## EMS HA Monitors

The Event Monitoring Service (EMS) is a free set of monitoring functions for HP-UX systems. In addition to free library routines for creating your own monitors, EMS provides a set of free monitors when you purchase a system. These include hardware diagnostic monitors. More sophisticated monitors are provided with the EMS HA Monitors product, which includes a disk monitor and a database monitor, as well as other monitors.

The database monitor included in the EMS HA Monitors product currently supports only Oracle environments. Both database and database server information is provided. One set of database resources is provided for each configured database (see Table 8-3), and one set of database server resources is provided for each active database server (see Table 8-4).

The EMS Database Monitor can detect changes in the state of a database, and can send events before the database runs out of critical database resources. With this monitor, MC/ServiceGuard can detect a database problem before failure and start recovery actions sooner, such as restarting a package on an alternate node.

The status field can be used to determine whether the database is functioning properly. The other fields in the table provide information on the amount of disk space available for the database.

As mentioned earlier, process information obtained from ps or other commands can indicate whether a database instance is running or has failed. Status information obtained from EMS can give more detailed information, such as whether the server is congested or whether the transaction rate is below an acceptable value. The EMS database monitor is focused on fault management,