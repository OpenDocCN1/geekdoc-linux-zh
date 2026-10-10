+   5. Click **Next** to continue. You are presented with an introduction to Active Directory Domain Services that provides a number of helpful hints for installing and administering Active Directory. The tips include the following points:
+   * Be sure to install more than one domain controller in each Active Directory domain so that clients can log on even if a single domain controller fails.
+   * Active Directory requires an available DNS server on the network.
+   * Installing Active Directory will also add the following prerequisite services to the server: **DFS Namespace**, **DFS Replication**, and the **File Replication Service**.

+   6. Click **Next** after you read the Introduction to AD Domain Services window.

+   7. Click **Install** to begin the installation process. The Server Manager *will appear to pause for a few minutes* because the actual executable files or *binaries* that are needed to install Active Directory are being copied to the system drive. A significant security improvement in Windows Server 2008 is that these binaries (installation files) are not actually installed until you choose to install Active Directory; this prevents any viruses or worms from targeting these files if the server is not configured as a domain controller because the files in question are not present on the hard disk.

+   8. After the AD DS binaries have installed, click **Close**. You are returned to Server Manager, which will now resemble the window shown in Figure 2-3. Notice that the Active Directory Domain Services role is listed, but it has a red *X* next to it. This indicates that the AD DS binaries have been installed on the server, but Active Directory has not been completely configured.

# Figure 2-3
Active Directory Domain Services role installed but not configured

![](bbox=[0.24, 0.47, 0.9, 0.82])

> Active Directory Domain Services
> role installed