Figure 4-35 Runlevel editing in expert mode.

6. Enable XDM to be run on levels 2, 3 and 5. Click Finish to complete the process.

These steps should do the trick. The next time, and when you log in with a VNC client, you will see a KDM login window.

For more information about the peculiarities of a Linux installation, which we do not mention in this book, read the Gentoo handbook¹¹ at:

http://www.gentoo.org/doc/en/handbook/index.xml

¹¹ Although this is the handbook of a specific Linux distribution, the concepts behind a Linux installation are very well outlined and generic.

# System Services (Runlevel): Details

Simple Mode
Expert Mode
Set default runlevel after booting to:
3. Full multiuser with network

Assign system services to runlevels by selecting the list entry of the respective service then checking or unchecking the check boxes B-5 for the runlevel.

Start/Stop/Refresh: Use this to start or stop services individually.

Set and Reset: Select runlevels in which to run the currently selected service.

+   - Enable the service: Activates the service in the standard runlevels
+   - Disable the service: Deactivates service.
+   - Enable all services: Activates all services in their standard runlevels

Changes to the default runlevel will take effect next time you boot your computer.

Service | Running | B | 0 | 1 | 2 | 3 | 5 | 6 | S | Description
smb | No |  |  |  |  |  |  |  |  | Samba SMB
smbfs | No |  |  |  |  | 3 | 5 |  |  | Import remote
smpppd | No |  |  |  |  |  |  |  |  | Start the smpp
snmpd | No |  |  |  |  |  |  |  |  | start netsnmp
splash | No |  |  | 1 | 2 | 3 | 5 |  | S | Splash screen
splash_early | Yes |  |  |  | 2 | 3 | 5 |  |  | kills animatio
squid | No |  |  |  |  |  |  |  |  | Squid web ca
sshd | Yes |  |  |  |  | 3 | 5 |  |  | Start the sshd
svcgssd | No |  |  |  |  |  |  |  |  | Start the RPC
syslog | Yes |  |  |  | 2 | 3 | 5 |  |  | Start the syste
vmlo... | Yes |  |  |  |  |  |  |  |  | Start the Linu
winbind | No |  |  |  |  |  |  |  |  | NSS daemon
xdm | Yes |  |  |  | 1 | 3 | 5 |  |  | X Display Ma

X Display Manager