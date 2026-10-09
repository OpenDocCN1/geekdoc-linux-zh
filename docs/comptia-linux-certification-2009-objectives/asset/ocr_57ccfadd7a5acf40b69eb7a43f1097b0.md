# How to Configure NIS

# Procedure Reference: Install an NIS Server

To install an NIS server:

+   1. Log in as root.
2. Mount the Linux installation media that contains the RPMs for the NIS server.

![](bbox=[0.04, 0.19, 0.75, 0.28])

+   3. Navigate to the /media/[name of the media]/Packages directory.
4. Install the ypserv, yp-tools, and ypbind packages using the commands.
   - `rpm -ivh ypserv*.rpm`
   - `rpm -ivh yp-tools-*.rpm`
   - `rpm -ivh ypbind*.rpm`
5. Verify that the packages have been installed.
   - `rpm -qi package name`

# Procedure Reference: Configure an NIS Server

To configure an NIS server:

+   1. Add the NIS domain name to the network file.
   a. Open the /etc/sysconfig/network file.
   b. Add the NISDOMAIN statement, specifying the NIS domain name.
      - `NISDOMAIN=domain name`
   c. Save and close the file.
2. Add NIS server information to the yp.conf file.
   a. Open the /etc/yp.conf file.
   b. Add the domain name in one of the three formats:
      - `domain domain name server server's host name`
      - `ypserver server's host name`
      - `domain domain name broadcast`
   c. Save and close the file.
3. Restart the portmap daemon to inform the NIS client about the ports on which the NIS server will be listening to requests.
   - `service portmap restart`
4. Enter service yppasswdd start to start the yppasswdd daemon and service new password requests from NIS users.