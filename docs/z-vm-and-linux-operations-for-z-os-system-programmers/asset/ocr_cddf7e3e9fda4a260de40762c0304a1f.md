# Checking system level: `query cplevel` and `query cmslevel`

The QUERY CPLEVEL and QUERY CMSLEVEL commands are useful for ensuring maintenance has been correctly applied on each system. The commands can be used to check the following items:

+   - Software version level, release level, and release modification level
+   - Software service level number
+   - Date and time (translated to the current active time zone) that CP system software was written to DASD
+   - Date and time CP was last started
+   - Release and service level of CMS

An example of the commands is shown in Example 5-2.

*Example 5-2　Checking CP and CMS levels*

```text
q cplevel
z/VM Version 5 Release 3.0, service level 0701 (64-bit)
Generated at 05/29/07 23:21:12 EDT
IPL at 06/11/08 07:58:34 EDT
Ready; T=01/0.01 11:45:20
q cmslevel
CMS Level 23, Service Level 701
Ready; T=01/0.01 11:45:24
```

# Checking CP load parameters: `query cpload`

Use QUERY CPLOAD, shown in Example 5-3, to display information regarding the last CP IPL. The information displayed includes the location of the CP module that was last used, the location of the parm disk, and how CP was started.

*Example 5-3　Querying CPLOAD*

```text
q cpload
Module CPLOAD was loaded from minidisk on volume LX6RES at cylinder 39.
Parm disk number 1 is on volume LX6RES, cylinders 39 through 158.
Last start was a system IPL.
Ready; T=01/0.01 11:46:07
```

# Checking the amount of real storage: `query storage`

The QUERY STORAGE command (abbreviated as Q STO) is used to display the amount of real memory that is available to an LPAR after it is started. See Example 5-4 on page 239.