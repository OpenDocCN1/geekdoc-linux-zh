quickly determine whether an increase in the number of concurrent users has occurred. It can also be useful in checking for security intrusions, because you may notice an unexpected user.

# # Using System Instrumentation

Standards for network and system management, such as the Simple Network Management Protocol (SNMP) and Desktop Management Interface (DMI), were developed to help make management easier. They provide industry-standard ways to build instrumentation and interface into the instrumentation, respectively. SNMP is used to access Management Information Bases (MIBs), and DMI is used to access Management Information Formats (MIFs).

Standard MIBs and MIFs define the metrics that can be used by any vendor’s instrumentation. Vendor-specific MIBs and MIFs provide vendor-specific instrumentation. This section looks at some of the system instrumentation available through each of these standards.

Many tools already exist for accessing this instrumentation. Several vendors offer browsers and monitoring capabilities that use a common interface to access instrumented objects from different hardware platforms and operating systems. For example, the common enterprise management frameworks, such as the HP Network Node Manager, include a MIB Browser tool to access MIB data. They may also include tools that can be used to monitor MIB data on remote systems from the enterprise management platform. Toolkits are available that provide an interface with which people can write their own tools to monitor or track this information. Furthermore, toolkits exist for creating your own instrumentation.

Many valuable system resources can be monitored via these standard interfaces, to detect system events or faults. Some of the resources that you may be interested in are reviewed in this section.

# ## SNMP

A MIB is a standard way of representing information of a certain category. For example, MIB-II provides useful information about a system, such as the number of active TCP connections, system hardware and version information, and so forth. OpenView IT/Operations (IT/O), discussed later in this chapter, provides a MIB Browser. The MIB Browser tool helps you to discover which MIBs are available, and to see the information being provided by each MIB. The MIB Browser tool can check the value of anything contained in a MIB. If you find a MIB that contains some useful fields, you can use the MIB Browser to gather that data from the target system. The resulting data is displayed in the MIB Browser’s output window on the screen. By browsing through available MIBs, and by querying values of selected MIB fields, you can gather specific information needed to monitor systems and troubleshoot problems.

The SNMP interface provides access to objects stored in various MIBs. MIB-II is a standard MIB that has been implemented on most UNIX systems. On HP-UX systems, the HP-UNIX MIB defines various metrics for monitoring system resources. Other vendors, such as Sun, have vendor-specific MIBs that provide similar information. Appendix A includes complete MIB definitions.