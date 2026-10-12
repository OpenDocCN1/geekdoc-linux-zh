Besides the values described here, you can access dozens more options by clicking the Advanced View button. When you have filled in all the fields you need, click Commit Changes on the screen to have the changes written to the `/etc/samba/smb.conf` file.

# Configuring shared directories with SWAT

To make your shared directory available to others, you can add an entry to the SWAT window. To use SWAT to set up Samba to share directories, do the following:

> **NOTE:** You may see one or more security warnings during the course of this procedure. These messages warn you that someone can potentially view the data you are sending to SWAT. If you are working on your local host or on a private LAN, the risk is minimal.

+   1. From the main SWAT window, click the **SHARES** button.

+   2. Type the name of the directory that you want to share in the **Create Share** box, then click **Create Share**.

+   3. Click **Advanced** to change to the Advanced view.

+   4. There are a few dozen options to choose from. Here are a few that might particularly interest you:

+   • **comment** — A few words to describe the shared directory (optional).

+   • **path** — The path name of the directory you are sharing.

+   • **read only** — If Yes, then files can only be read from this file system, but no remote user can save or modify files on the file system. Select No if you want users to be allowed to save files to this directory over the network.

+   • **guest ok** — Select Yes to enable anyone access to this directory without requiring a password.

+   • **hosts allow** — Add the names of the computers that will be allowed to access this file system. You can separate host names by commas, spaces, or tabs. Here are some valid ways of entering host names:

+     - **localhost** — Allow access to the local host.

+     - **192.168.74.18** — IP address. Enter an individual IP address.

+     - **192.168.74.** — Enter a network address to include all hosts on a network. (Be sure to put a dot at the end of the network number or it won’t work!)

+     - **maple, pine** — Enable access to individual hosts by name.

+     - **EXCEPT host** — If you are allowing access to a group of hosts (such as by entering a network address), use EXCEPT to specifically deny access from one host from that group.