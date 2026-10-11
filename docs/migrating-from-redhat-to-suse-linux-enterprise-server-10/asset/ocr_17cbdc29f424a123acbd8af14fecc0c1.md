# SUSE Linux Enterprise Server 10

SUSE Linux Enterprise Server 10 can be configured as iSCSI target and as iSCSI initiator. You can do this with the configuration tool YaST or manually.

+   - Set up an iSCSI Target
+   - Set up an iSCSI Initiator
+   - Mount iSCSI Targets Automatically at Boot Time

# Set up an iSCSI Target

You can either start YaST and select **Network Services > iSCSI Target**, or start the iSCSI Target module directly by entering as root in a console window **yast2 iscsi-server**.

If the iscsitarget package is not installed, YaST will invite you to do that:

![](bbox=[0.1, 0.53, 0.89, 0.85])