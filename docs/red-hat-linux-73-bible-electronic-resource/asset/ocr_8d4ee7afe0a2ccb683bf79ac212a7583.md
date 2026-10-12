The installed *portsentry* package consists of several configuration files (in the */etc/portsentry* directory), the *portsentry* start-up script (*/etc/init.d/portsentry*), and the *portsentry* command (in */usr/sbin*). There are also **README** files of interest in the */usr/share/doc/portsentry\** directory.

# # Using PortSentry as is

As with **Logcheck**, you don’t need to do anything to get **PortSentry** to work after it is installed. By default, here is what **PortSentry** does when you install the *portsentry* package:

+   - The */etc/init.d/portsentry* start-up script runs automatically when you boot to run levels 3, 4, or 5 (levels 3 and 5 are most commonly used).
+   - The following port numbers are configured to be monitored by **PortSentry** in basic mode:
+   	**TCP:** 1, 11, 15, 143, 540, 635, 1080, 1524, 2000, 5742, 6667, 12345, 12346, 20034, 31337, 32771, 32772, 32773, 32774, 40421, 49724, 54320
+   	**UDP:** 1, 513, 635, 640, 641, 700, 32770, 32771, 32772, 32773, 32774, 31337, 54321
+   - In response to attacks (represented by scans of the ports being monitored), all further attempts to connect to any services for the protocol (**TCP** or **UDP**) will be blocked.

The computers that are blocked from accessing your system are listed in either the *portsentry.blocked.tcp* or *portsentry.blocked.udp* files (in the */var/portsentry* directory), depending on which protocol was scanned (**TCP** or **UPD**). Removing entries from these files to restore access to blocked computers.

# # Configuring PortSentry

Chances are that you will want to make some changes to the way that **PortSentry** runs. To change how **PortSentry** behaves, modify the */etc/portsentry/portsentry.conf* file. In that file, you can choose which ports to monitor, the mode in which to monitor, and the responses to take when a scan is detected. The responses can include:

+   - Blocking access by the remote computer
+   - Rerouting messages from the remote computer to a dead host
+   - Adding a firewall rule to drop packets from the remote computer

The only other file you may want to change is the */etc/portsentry/portsentry.modes*. The *portsentry.modes* file simply contains the modes that **PortSentry** can be run in.