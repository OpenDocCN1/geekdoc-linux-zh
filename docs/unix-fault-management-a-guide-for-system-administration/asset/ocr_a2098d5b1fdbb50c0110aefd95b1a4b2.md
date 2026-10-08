are developed in a common way. Although the framework itself is freely available, some EMS monitors are sold separately, shipped with the products they support, or bundled with the system.

EMS monitors provide help primarily with fault and resource management. Performance monitoring generally requires more sophisticated tools. Some system fault and resource monitoring capabilities are provided by the HA Monitors product and EMS Hardware Monitors. Other EMS monitors enable you to detect when you are getting low on system resources, such as file descriptors, shared memory, and system semaphores.

# Monitored Components

Multiple HP products include specific EMS resource monitors, so the resources available for monitoring vary depending on the customer’s installed software products. The resources available for monitoring also vary from system to system because the hardware configuration is different.

EMS Hardware Monitors are provided with the Online Diagnostics bundle, available on the HP-UX support media, also known as the HP-UX Diagnostic/IPR Media. EMS Hardware Monitors provide the ability to detect and report problems with system hardware resources, such as device errors and component failures. Monitors are available for system hardware components and various HP storage products, including system memory, SCSI disk and tape devices, AutoRAID disk arrays, high availability disk arrays and storage systems, fast/wide SCSI disk arrays, various fibre channel components, tape autoloaders, and digital linear tapes.

The HA Monitors contain several EMS monitors for monitoring filesystem space, network interface status, disk status, and MC/ServiceGuard cluster status. HA Monitors also provide monitoring for CPU load and the number of system users. The monitors include database monitoring as well.

ATM adapters and HyperFabric adapters from HP can also be monitored using EMS. An EMS monitor is included with each of these products. These resources are also integrated with MC/ServiceGuard. HA ATM, for example, first attempts to perform a local recovery in the event of a failure, but if it is unable to provide local recovery, it notifies MC/ServiceGuard to trigger a failover to an alternate node.

All the different resources that can be monitored are contained in a single EMS resource hierarchy. The portion of the hierarchy containing system hardware and kernel resources is shown in Figure 3-3. You see the entire resource hierarchy when configuring monitor requests in the EMS GUI.

# Monitoring Features

EMS is designed for use in high availability environments. The user can select only the critical components to be monitored, so the resource monitor will not be delayed polling for information from non-critical components. This is different from other tools, such as IT/O, which typically gathers data from all components. The IT/O agent executes a system-wide command and then parses the output. Thus, if a noncritical component hangs, the IT/O agent could be delayed