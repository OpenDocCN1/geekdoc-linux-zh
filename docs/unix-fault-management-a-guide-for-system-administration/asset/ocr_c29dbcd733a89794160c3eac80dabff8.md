```
Listing A-5  Continued

```
[ 8 ] prtOutputDimensionsGroup
[ 9 ] prtOutputFeaturesGroup
[10 ] prtMarkerGroup
[11 ] prtMarkerSuppliesGroup
[12 ] prtMarkerColorantGroup
[13 ] prtMediaPathGroup
[14 ] prtChannelGroup
[15 ] prtInterpreterGroup
[16 ] prtConsoleGroup
[17 ] prtAlertTableGroup
[18 ] prtAlertTimeGroup
[ 1 ] prtMIBCompliance
```
```

# ### Monitoring Notes

If you intend to write your own SNMP application, the numeric root OID of the Printer MIB is 1.3.6.1.2.1.43.

The Printer MIB requires portions of the MIB-II and the Host Resources MIB to be implemented. Many of the tables in the Printer MIB are indexed by hrDeviceIndex, from the Host Resources MIB.

The hrDeviceStatus field in the hrDeviceTable is combined with the hrPrinterStatus and hrPrinterDetectedErrorState fields in the hrPrinterTable to determine the specific status of a printer device. For example, if the hrPrinterStatus indicates an idle status and the hrDeviceStatus indicates a running status, then the corresponding printer is functioning normally. However, if the hrPrinterStatus is idle and the hrDeviceStatus indicates a warning status, then the printer has a status of noncritical alert active.

The prtAlertTable can record the list of alerts occurring for a printer device. The prtAlertCode indicates the specific printer problem, such as a paper jam, a paper tray missing, or low toner.

# ### The HP-UNIX MIB

The HP-UNIX MIB is a private MIB provided by Hewlett-Packard. It is meant to be an extension to the MIB-II. The HP-UNIX MIB contains important information about the users, jobs, filesystems, memory, and processes of a system. The number of users logged in to the system and the number of jobs running are both indications of how busy the system is. The amount of free swap space or filesystem space can be a warning of potential problems. The process status can be checked to see whether a particular application is still running normally on the target system.

# ### MIB Definition

Listing A-6 shows the complete specification for the HP-UNIX MIB, as defined by Hewlett-Packard.