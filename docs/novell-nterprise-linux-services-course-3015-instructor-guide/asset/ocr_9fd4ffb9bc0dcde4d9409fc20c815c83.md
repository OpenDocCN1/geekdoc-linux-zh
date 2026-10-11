+   - Which server(s) will host NetMail agents?
+   - Which agents will be located on a given server?
+   - Which domains will be serviced by each messaging server?
+   - Does your organization need fault tolerance and scalability by deploying the same agents on multiple servers?

# Meet System Requirements

To install NetMail, you must meet the following system requirements:

+   - Make sure you're running 1 of the following:
+   
+     - Red Hat® Linux AS 2.1
+     - Red Hat Linux ES 2.1
+     - SuSE® SLES 8
+   - Make sure eDirectory 8.7.3 or later for Linux is installed.
+   - Make sure your system CPU is at least a 750 MHz Pentium® III or Athlon.
+   - Make sure you have at least 512 MB of system RAM.
+   - Make sure you have 20 MB of disk space free for installation. Disk space for the NetMail message store varies, based on the number of users and the amount of disk space allowed per mailbox.
+   - Each server hosting a NetMail service must have an eDirectory replica of the partition containing the users who will use the messaging service.
+   - Make sure the eDirectory tree is synchronized and healthy.
+   - Make sure you have Admin rights to the eDirectory tree where you plan to install NetMail.