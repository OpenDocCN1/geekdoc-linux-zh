# Configuration Events

You should know about the hardware and software configuration changes taking place on your servers. A software package installed just days before a failure may be a prime suspect. Configuration changes can be complex, and administrative tools often do not provide adequate assistance. Operator error is a common source of unplanned downtime, so it is important to keep a record of the configuration changes, as well as the time each change is made. This log can be examined later, in the event of a problem, to provide an audit trail for backing out of the changes. This can be especially important when multiple operators make changes on the same systems.

Configuration changes encompass a broad spectrum, and they may involve the application or database, operating system, or system hardware or peripherals.

# Application Changes

Application changes include changing software parameters, such as the maximum number of users allowed to use a product. Restructuring a database is another example. Keeping a history of the changes made to application parameters can be difficult, and probably is done most commonly through revision comments in the configuration files themselves. Patches or bug fixes to applications are easier to track because the software includes a version number, which should be updated by the software vendor whenever new versions are released. Numerous tools are now available to track the software versions installed on your system. You should run one of these tools periodically and store the results, to maintain an appropriate change history.

Installing a new application on the server is a key event that should be recorded. You should use this application in a test environment before moving it to production. However, the application still might not behave well. You may want to use this time as a data point when looking at performance data, to see the effect of the new application.

# Operating System Changes

Operating system changes are usually easier to track because they often require a system reboot before they take effect. Enterprise management products, such as HP OpenView, automatically record system reboots as events in an event log. Operating system configuration changes include changes to kernel parameters, patches, and operating system upgrades. All of these changes should be recorded.

# Hardware Changes

Hardware configuration changes include the addition of a new processor or a new disk device. You may also want to remove or replace a component that is not behaving properly. Other hardware configuration changes include changing the firmware versions or patching the driver software.

Because these configuration changes often involve a system reboot, you should plan for downtime and schedule changes during a period when the systems are not being used. Planned downtime includes downtime required for scheduled maintenance, such as a software upgrade, and for configuration changes, such as adding disks, restructuring a database, or moving clients to different systems for load-balancing purposes.