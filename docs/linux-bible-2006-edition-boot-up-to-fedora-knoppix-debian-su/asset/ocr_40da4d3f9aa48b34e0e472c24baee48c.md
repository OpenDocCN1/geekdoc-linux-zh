# Domain master — Set this to Yes if you want the Samba server (nmbd daemon) to identify itself as the domain master browser for your workgroup. This list will allow client computers assigned to the workgroup to use SMB-shared files and printers from subnetworks that are outside your own subnet. This is set to No by default.

If browsing is not working, check the nmbd log file (/var/log/samba/log,nmbd). To get more detail, increase the debug level to 2 or 3 (described earlier in this section) and restart Samba. The log can tell you if your Samba server is the master browser and, if so, computers are on its list.

# WINS Options

Use the WINS options if you want to have a particular WINS server provide the name-to-address translation of NetBIOS names used by SMB clients:

+   server — If there is a WINS server on your network that you want to resolve the NetBIOS names for your workgroup, enter that server's IP address here. Again, you probably use a WINS server if your workgroup extends outside the local subnet.

+   support — Set this value to Yes if you want your Samba server to act as a WINS server. (It's No by default.) Again, it is not needed if all the computers in your workgroup are on the same subnet. Only one computer on your network should be assigned as the WINS server.

In addition to the values described here, you can access dozens more options by clicking the Advanced View. When you have filled in all the fields you need, click Commit Changes on the screen to have the changes written to the /etc/samba/smb.conf file.

# Configuring Shared Directories with SWAT

To make your shared directory available to others, add an entry to the SWAT win-directory. To use SWAT to set up Samba share directories, do the following:

You may see one or more security warnings during the course of this procedure. These messages warn you that someone could potentially view the data you are sending to SWAT. If you are working on your local host or on a private LAN, the risk is minimal.

+   1. From the main SWAT window, click the SHARES button.
2. Type the name of the directory you want to share in the Create Share box, and then click Create Share.
3. Add any of these options:
Comment — A few words to describe the shared directory (optional).
Path — The path name of the directory you are sharing.