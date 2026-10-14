3. The Auditing tab allows you to specify a log file and operations to be logged. The Files Attributes tab allows you to configure the lock daemon and FAT filesystem.

# Configuring the NFS Gateway

Setting up the gateway for NFS is very similar to the NFS server configuration procedure.

+   1. Click Gateway for NFS to configure the server as a gateway. You will need to enter the Windows domain and NIS domain information, check Implicit Mapping and Display Implicit Maps, and then click Get UNIX Accounts.

+   2. Now the Windows Users in the Explicit Mapping section should have UIDs and GIDs from the NIS domain. Like the server, there is also a manual procedure for mapping different user names between Windows and UNIX NIS domains. Next, click the Sharing tab, and then click the Launch Sharing utility. The Gateway for NFS Shares window pops up (Figure 8.7).

![](bbox=[0.22, 0.64, 0.9, 0.92])

Figure 8.7 Gateway for NFS Share window.