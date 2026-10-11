+   7. In the **Server** field, browse to and select the server you want to associate with the **Driver Set** object.

+   8. Check **Create a new partition on this driver set**.

+   9. Click **Next**. The screen shown earlier in Figure 7.9 appears.

+   10. Mark **Import a pre-configured driver from the server (XML file)**.

+   11. From the drop-down list, select the **eDIR-Driver.xml** driver.

+   12. Click **Next**. The screen shown in Figure 7.22 appears.

![](bbox=[0.26, 0.29, 0.94, 0.54])

+   13. In the **Driver Name** field, enter a name for this driver.

+   14. In the **Remote Tree Address** and **Port** fields, enter the IP address of the server running DirXML in the remote tree. The port number should be set to **8196**.

+   15. In the **Configure Data Flow** drop-down list, select the role the local server will play. You have the following options:
+   	> **Bidirectional**—Selecting this option will configure the driver to send synchronization events to the remote tree and to accept incoming synchronization events.
+   	> **Authoritative**—Selecting this option will configure the driver to send synchronization events to the remote tree, but it will not accept incoming synchronization events.
+   	> **Subordinate**—Selecting this option will configure the driver to accept incoming synchronization events, but not to send them.

+   16. In the **Configuration Option** drop-down list, select the placement option you wish to use. You can select from the following:
+   	> Mirrored

![](bbox=[0.03, 0.29, 0.25, 0.36])