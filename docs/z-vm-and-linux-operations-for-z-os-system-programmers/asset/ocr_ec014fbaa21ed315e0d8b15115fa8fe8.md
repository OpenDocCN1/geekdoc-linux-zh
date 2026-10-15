```
'cp set mdc stor 0m 128m' /* Limit minidisk cache in CSTOR */
'cp set mdc xstore 0m 0m' /* Disable minidisk cache in XSTOR */
'cp set srm storbuf 300% 250% 200%' /* Overcommit memory */
'cp set signal shutdown 180' /* Allow guests 3 min to shut down */
'cp logoff' /* logoff when done */
```

4. Save your changes with the FILE subcommand.

> Important: The set mdc and set srm lines are z/VM tuning values. These are likely good starts for Linux systems, but might not be optimal. To read more about these values see the following Web sites:
> 
> http://www.vm.ibm.com/perf/tips/linuxperf.html
> 
> http://www.vm.ibm.com/perf/tips/prgmdcar.html

Your system should now be configured to start up the virtual switches and send a signal to shut down Linux virtual machines gracefully.

# Verifying the changes

It is now time to make these changes take effect. You can do that by re-IPLing the system again or by issuing the commands you just placed into AUTOLOG1's profile. To re-IPL, pass the parameter IPLPARMS CONS=SYS C to the SHUTDOWN REIPL command:

```
==> shutdown reipl iplparms cons=sysc
```

Although you lose your session, it should be back up in several minutes. When it is back up, perform the following steps:

+   1. Start a 3270 session and Logon as MAINT.
+   
+   2. Query the new VSWITCH:

```
VSWITCH SYSTEM VSW1 Type: VSWITCH Connected: 0 Maxconn: INFINITE
PERSISTENT RESTRICTED NONROUTER Accounting: OFF
VLAN Unaware
State: Ready
IPTimout: 5 QueueStorage: 8
Portname: UNASSIGNED RDEV: 3024 Controller: DTCVSW1 VDEV: 3024
Portname: UNASSIGNED RDEV: 3028 Controller: DTCVSW2 VDEV: 3028 BACKUP
```

Verify that the VSWITCH exists and that there are two built-in VSWITCH controllers, DTCVSW1 and DTCVSW2. Before z/VM version 5.2, these user IDs had to be created manually.