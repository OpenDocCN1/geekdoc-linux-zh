points along the boot process, think of it as both a wakeup call and a snooze button. To illustrate, here’s how one author’s wife gets up for work in the morning:

She sets the alarm for 5:30 AM. When the alarm goes off, she hits the snooze button deciding to cuddle for 15 minutes (callback number 1). At 5:45 AM, callback number 2 is reached; she rolls over and hits the snooze button again for a 15-minute pre-shower-power-nap. Finally, at 6:00 AM, the last callback is triggered as the alarm sounds to indicate it’s time to get on with the day.

Callback routines are triggered when particular dispatch points are reached. Additionally, some subsystems must be configured before or after other subsystems at the same dispatch point, so callback routines can also be registered at a specified priority to insure that callbacks are called in the proper order. When a dispatch point is reached, all subsystem callbacks, registered for that dispatch point, will be executed in order of priority. Callback dispatch points are defined in the sysconfig.h file located in the /sys/include/sys directory.

We will not discuss what happens at each and every dispatch point but instead, in Table 17.5 we will show you the boot messages you will likely see (if any) as the various cluster and cluster-related subsystems are configured. These messages will appear on the system’s console as well as the messages file in the /var/adm directory.

For more information regarding a particular subsystem, you can consult the sys_attrs_subsystem reference page.

# 17.6  Configuring the Connection Manager

When a system that has been configured to run in a cluster is booted, it will perform the following steps when the Connection Manager is configured.

+   - Initialize data structures including the cluster membership list.
+   - Create the main CNX transaction thread (“csb event thread”).
+     - Set a wakeup call for 10 seconds. Try to form a cluster when timeout is reached.
+   - Create the remote communication threads (“wait for csb”). There are currently 7 threads.
+   - Create the grim reaper thread (“cnx grim reaper”).
+   - Create the CNX pinger thread (“cnx pinger”).
+   - If a quorum disk is configured, start the quorum disk thread (“qdisk tick delay”).

As you can see, at this point the CNX has several threads running and theoretically doing things simultaneously. However, certain things (more or less) need to occur in a sequential order.