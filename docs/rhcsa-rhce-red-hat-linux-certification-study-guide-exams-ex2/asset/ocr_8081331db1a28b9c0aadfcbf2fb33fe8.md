# EXERCISE 5-3

# Modify Network Interfaces with the Network Connections Tool

This exercise depends on the active use of the NetworkManager service, and the accompanying GUI configuration tool. You'll see what's added to the key configuration file, courtesy of the noted tool.

+   1. Back up the configuration for the network card to be changed. If it's the first Ethernet card, back up the ifcfg-eth0 file from the /etc/sysconfig/network-scripts directory. Make sure a copy of the file exists in both directories.
+   2. Start the Network Connections tool. From a GUI terminal, press ALT+F2, and enter nm-connection-editor in the text box that appears. This opens the Network Connections tool.
+   3. Select the Wired tab if it isn't already active.
+   4. Select the adapter that you want to modify, and then click Edit. If it is an Ethernet adapter, you'll see an Editing System window similar to the one shown in the next illustration.

![](bbox=[0.28, 0.55, 0.85, 0.88])