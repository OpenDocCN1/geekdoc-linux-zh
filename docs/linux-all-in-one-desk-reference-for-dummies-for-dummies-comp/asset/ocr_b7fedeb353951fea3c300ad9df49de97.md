+   - smbadduser: This program adds users to the SMB (Server Message Block) password file.
+   - smbcacIs: This program manipulates Windows NT access control lists (ACLs) on shared files.
+   - smbclient: This is the Windows client, which runs on Linux and allows Linux to access the files and printer on any Windows server.
+   - smbcontrol: This program sends messages to the smbd, nmbd, or winbindd processes.
+   - smbd: This is the SMB server, which accepts connections from Windows clients and provides file-sharing and print-sharing services.
+   - smbmount: This program mounts a Samba share directory on a Linux PC.
+   - smbpasswd: This program changes the password for an SMB user.
+   - smbprint: This script enables printing on a printer on an SMB server.
+   - smbstatus: This command lists the current SMB connections for the local host.
+   - smbta: This program backs up SMB shares directly to tape drives on the Linux system.
+   - smbunmount: This program unmounts a currently mounted Samba share directory.
+   - testparm: This program ensures that the Samba configuration file is correct.
+   - winbindd: This server resolves names from Windows NT servers.

In the following sections, I describe how to configure and use Samba.

# # Installing Samba

You may have already installed Samba when you installed Linux. You can check first, and if you don't find Samba on your system, you can easily install it.

![](bbox=[0.11, 0.72, 0.21, 0.81])

In Debian, MEPIS, Ubuntu, and Xandros, type `dpkg -l samba*` to see if Samba is installed. In Fedora Core and SUSE, type `rpm -q samba` to see if the samba package is installed.

![](bbox=[0.11, 0.82, 0.21, 0.91])

In Debian, MEPIS, and Ubuntu, type `apt-get install samba` to install Samba. In Fedora Core, log in as root, mount the DVD, and type `cd /media/cdrom/Fedora/RPMS` followed by `rpm -vh samba*`. In SUSE, click Software Management in the YaST Control Center’s Software category. Then use YaST’s search facility to look for `samba`, select the relevant packages, and install them. As for Xandros, you get Samba when you install Xandros.