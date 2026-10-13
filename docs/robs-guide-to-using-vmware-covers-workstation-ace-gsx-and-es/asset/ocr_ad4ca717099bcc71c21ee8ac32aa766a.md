The best thing to do is to either take all (or all but one) of the servers in the cluster off-line, and then suspend all of them; or, just shut down the operating system and power off the virtual machines.

# 28.2 No Shared Media is Available

If during the cluster installation the software reports that no shared media is available, there are three known common problems:

+   1. The servers do not have access to the shared disk. Check with `list devices` to find out whether both servers can see the shared disk.
+   
+   2. One of the servers does not have the `disk.locking = "false"` line in the `.VMX` file. In this scenario, one of the servers does not lock the disk and the second one does, which prevents the other server to write to the disk.
+   
+   3. There is data on the disk that prevents the Cluster Services installation from creating the Split Brain Detector (SBD) partition. In this case, replace the disk with a new one or use the NSS Management Utility (NSSMU .NLM) to initialize the disk. This is shown in Figure 28.10.

![](bbox=[0.15, 0.62, 0.9, 0.82])

Figure 28.10: The shared disk can be initialized with the NSS Management Utility