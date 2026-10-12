# Samba in Centennial’s Heterogeneous Environment

The developers of Samba created a set of programs that allows UNIX and UNIX-like operating systems like Linux to communicate with Microsoft hosts. Microsoft uses a protocol known as NetBEUI, which implements server message blocks for network communication. Since many of Centennial’s workstations ran Windows 95/98, implementing Samba became necessary in order to use Linux.

# Training the Centennial Team

To provide an example of how Bynari coached the Centennial team, we’ll use the Samba configuration to demonstrate Bynari’s methodology. Mike Caron explains:

> > We began the samba install initially without setting up the server as an NT domain server. We learned how to create Linux users, and how to make samba users from existing Linux users. We then edited the /etc/hosts file to include the ip numbers of our samba client boxes. This was done because we were not ready to implement DNS services in our test lan. The smb.conf was then edited to set up disk shares.

> > The following steps are a general guideline we used for installing Samba and creating an NT Domain on a Linux Server.

+   - The very first step is to download the most current stable RPM for Samba and then install it. `rpm -Uvh <rpm name>` (The "U" is for "upgrade")
+   - Next create a public directory, and use chmod to give all users full access.
+   - We mkdir /home/pub and then chmod /home/pub 777.
+   - We edited /etc/hosts and created a public share for the /home/pub directory.
+   - We copied a template smb.conf file to the /etc directory and edited it to the specific server, domain name and any other specific settings.
+   - Now run linuxconf to edit some specific network settings for the server.
+   - Select Browse Master=yes, Local Master=yes, os level=65 (Later Domain Master=yes, os level=255)
+   - Select Synchronize Linux from SMB passwords (yes)
+   - Create Linux user, adduser if necessary and then create the Samba user smbadduser for any users that want access to this samba server.