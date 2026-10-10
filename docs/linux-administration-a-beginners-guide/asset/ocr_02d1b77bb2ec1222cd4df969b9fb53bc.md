# **Linux vs. Windows NT Shut Down Process**

# **Linux Shutdown**

![](bbox=[0.08, 0.18, 0.48, 0.58])

+   - Step 1: The shutdown or reboot command is invoked
+   - Step 2: Init is told to change to runlevel 6
+   - Step 3: The scripts in /runlevel 6 call init scripts with the parameter “Stop”
+   - Step 4: Outstanding buffers are written for disk (sync) 
+   - Step 5: The file systems are unmounted
+   - Step 6: The system is halted

# **NT Shutdown**

![](bbox=[0.55, 0.18, 0.95, 0.58])

+   - Step 1: The shutdown command is invoked
+   - Step 2: The WINS Server is notified that the machine is leaving the network
+   - Step 3: Disconnections from all network services
+   - Step 4: The persistent connection to the PDC is closed
+   - Step 5: “Last Know Good” information is written to the registry
+   - Step 6: Services are shutdown
+   - Step 7: The system is halted

Unfortunately, the Linux and NT shutdown procedures don't show the same amount of parallels that their boot processes do. This stems from the nature of Linux's NIS, NFS, and LPR services versus NT's PDC and SMB protocols. Linux doesn't maintain persistent connections for those services; NT does.