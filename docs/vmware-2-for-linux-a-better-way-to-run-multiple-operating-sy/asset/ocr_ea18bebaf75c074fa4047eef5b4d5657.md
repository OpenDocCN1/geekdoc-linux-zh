If you ever need to mount a virtual floppy file for use in a virtual machine, follow these steps:

+   1. Click on one of the virtual machine floppy drive slots.
+   2. Click on the Type tool and change it to File.
+   3. Enter the complete path to the virtual floppy file.
+   4. Click on the Install button to commit your change.
+   5. Save the new configuration by clicking Save at the bottom of the window. This also exits the Configuration Editor.

# Ethernet Adapters

Each virtual machine can have as many as three virtual network connections, although you are likely to need only one or two.

The wizard automatically configures Ethernet adapters based on the networking choice you made at the end of the wizard process (Bridged, Host, both, or neither).

If you passed on either the Bridged or Host networking, you can easily add it here by selecting the one you want from the Connection Type tool and clicking Install, on the window like the one shown in Figure 5.24. No configuration is necessary.

> If at all possible, allow the wizard to handle your network configuration.

![](bbox=[0.03, 0.79, 0.52, 0.92])

# Serial Ports

The Configuration Wizard does not set up any serial ports, but it is fairly easy to adjust if you need to use them. Although VMware supports three different types of