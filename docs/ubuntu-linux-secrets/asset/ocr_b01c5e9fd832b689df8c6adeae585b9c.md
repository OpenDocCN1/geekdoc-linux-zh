# Part 4: Using the Ubuntu Server

![](bbox=[0.177, 0.103, 0.889, 0.514])

**Figure 22-9:** The CUPS printer admin page.

# Summary

This chapter walked through how to set up your Ubuntu server to share folders and printers on a Microsoft Windows network. The Samba software package allows you to add your Ubuntu server to a Windows network as a member server or as a domain controller server. You can also have your Ubuntu server act as a standalone server in a Windows workgroup if you’re just operating on a small home network.

The chapter discussed how to modify the `smb.conf` configuration file to create a standalone server using the Ubuntu system user accounts to authenticate users and control permissions on the shared folders. The Ubuntu server can also work as a print server on networks using both Samba and the CUPS server software. The CUPS server provides a simple interface for controlling printers on the system. Its web interface allows you to control your printers from a graphical environment.

The next chapter continues our discussion of the Ubuntu server by examining the Postfix email server. You can create a full-featured email server for your network simply by changing a few configuration parameters!