# 14.6 My NetWare Server Keeps Losing Time Synchronization

Running multiple servers in VMware asks for time synchronization between your NetWare servers. You can set this up with the normal Timesync mechanism. It happens frequently that NetWare virtual machine configurations lose their time synchronization. If your NetWare servers keep losing their time synchronization, then change the synchronization parameters as follows:

+   - Set the Polling Interval to 3600
+   - Set the Short Interval to 600

The TID that explains these parameters is located at the end of this paragraph.

Note: Do not use NTP for time synchronization with NetWare and VMware. The normal Timesync synchronization (also via TCP/IP) that NetWare uses is sufficient for most configurations.

Note: After setting up time synchronization between the NetWare servers, do not enable the time synchronization that VMware offers between the host and the guest. Check this status in the VMware tools in the GUI or with the command VMWTOOL SYNCTIME.

The parameters described here only work with Timesync. On older versions of NetWare, you can use MONITOR.NLM (with !h switch to show hidden parameters). But in NetWare 5.1 and 6.x, you can use Remote Manager to show the hidden parameters and set them accordingly.

![](bbox=[0.05, 0.86, 0.95, 0.97])

Figure 14.3: NetWare time synchronization parameters.