# Attacking and Defending Windows 2000 • Chapter 5 217

111.114

Value = String Administrator

```
Variable = .iso.org.dod.internet.private.enterprises.lanmanager.
lanmgr-2.server.
svUserTable.svEntry.svUsername.14.73.85.83.92.65.98.68.87.50.75.65.
83.49
```

Value = String IUSR_EXCW2KAS1

```
Variable = .iso.org.dod.internet.private.enterprises.lanmanager.
lanmgr-2.server.
svUserTable.svEntry.svUsername.14.73.65.77.95.69.88.67.87.50.65.
83.49
```

Value = String IWAM_EXCW2KAS1

The string values in this example reflect the list of users defined on the domain controller being queried with the utility. SNMP has the capability to report information about numerous conditions on the network; it is not used only for controlling network devices. From this same command, it is also possible to see the enumeration of shares, which can provide another point of attack. This can be seen here:

```
Variable = .iso.org.dod.internet.private.enterprises.lanmanager.
lanmgr-2.server.
sShareTable.svEntry.svShareName.6.83.89.83.86.79
```

Value = String SYSLOG

```
Variable = .iso.org.dod.internet.private.enterprises.lanmanager.
lanmgr-2.server.
sShareTable.svEntry.svShareName.8.78.69.84.76.79.71.79
```

Value = String NETLOGON

```
Variable = .iso.org.dod.internet.private.enterprises.lanmanager.
lanmgr-2.server.
sShareTable.svEntry.svSharePath.3.77.79.67
```

Value = String E:\

```
Variable = .iso.org.dod.internet.private.enterprises.lanmanager.
lanmgr-2.server.
```

![](bbox=[0.708, 0.941, 0.932, 0.966])