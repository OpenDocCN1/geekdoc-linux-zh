# ## Peripherals Administration

The peripherals administration menu allows you to select from three sub-areas:

+   - **Keyboard Layout**—Allows you to change the keyboard map, key repeat rate, and key repeat delay.
+   - **Text Mode Mouse Configuration**—Allows you to change the GPM mouse model, driver, protocol, device file, emulation, and boot-time activation (yes or no). Unless you work on a VT (VC) a lot, you probably won’t be interested in this too much. The mouse under X is changed with a different tool you’ll learn about in a following section.
+   - **Printer Configuration**—Allows you to see what printer is configured on your system. This module lacks some functionality, though that is expected to change.

# ## Network Administration

The Network Administration subsystem is composed of five individual components:

+   - Common Network Functions
+   - Network Information Service
+   - TCP/IP Network Options
+   - Hostname Resolution
+   - Mail Transport Configuration

# ## Common Network Functions

The common network functions selection allows you to configure any known interface on your system. If you have a module loaded for it, you can configure it. You can also configure an alias here.

Any changes made to this particular interface will be made as soon as OK is selected.

# ## Network Information Service

This text does not delve into NIS. This text selection box would make it seem easy to set up NIS just by choosing a Domain Name (a NIS Domain Name, not your Internet Domain Name, although that could be used), the NIS Servers, and whether or not to start NIS at boot time.

Setting up a NIS server is just a little more complex than this simple Client Setup box would have you believe, and no server setup exists at the moment. If you feel you have a need to run a NIS server because your network is large and administration would be easier, read `/usr/doc/nis-server-2.0/README.server`. Then go to `/etc/nis/` and follow the six-step instructions carefully.