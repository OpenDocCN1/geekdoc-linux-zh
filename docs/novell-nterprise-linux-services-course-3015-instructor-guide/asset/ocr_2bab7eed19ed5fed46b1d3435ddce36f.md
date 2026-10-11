# ## Deafult NetStorage Access

The NetStorage Web page displays the network files and folders.

The following illustrates folders accessible by default from the NetStorage web page:

**Figure 6-17**

![](bbox=[0.32, 0.22, 0.91, 0.4])

The **shared** folder, shown in Figure 6-17, is a default NetStorage location that all users can access for uploading or downloading files. Users do not have to be Samba-enabled to access this folder.

NetStorage is automatically configured to give all eDirectory users access to the **shared** folder on your NNLS server. The path to this folder is

/var/opt/novell/netstorage/shared

# ## Additional Configured NetStorage Access

You can create folders that only specific users have access to. You do this by creating Storage Location objects that point to folders on Linux and NetWare servers.