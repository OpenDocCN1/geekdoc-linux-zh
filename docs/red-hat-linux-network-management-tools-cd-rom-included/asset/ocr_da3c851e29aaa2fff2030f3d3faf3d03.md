ing, these services amount to having a way to interrogate SNMP agents in an automated fashion.

# SNMP-Trouble Menu

The SNMP-Trouble menu, shown in Figure 11.42, provides options to query devices for specific information. When specific problems occur, use this menu to learn more about the problem and implement a solution.

![](bbox=[0.05, 0.29, 0.35, 0.55])

Figure 11.42 SNMP-Trouble menu.

The options in the SNMP-Trouble menu are described below.

# SNMP Devices

This option provides a generic test to determine which of the selected devices on the topology panel respond to SNMP requests. The system.SysDescr.0 MIB-II object is queried as a result of selecting this option. The option is provided as a quick way to establish basic SNMP connectivity to network devices.

# System Information

This option shows generic SNMP information about the target system. It provides the equivalent of a walk on the MIB-II system group, as shown in Figure 11.43.