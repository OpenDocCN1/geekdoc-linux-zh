# **init Scripts and Runlevel Directories**

/etc/inittab defines the runlevel the system uses after booting is complete. The services that need to be started in a certain runlevel are not defined in /etc/inittab itself. These are configured by symbolic links in directories /etc/init.d/rcx.d/ which point to scripts in /etc/init.d/. To be able to manage runlevels, you need to understand the following:

+   - init Scripts
+     - Runlevel Symbolic Links
+   - How init Determines which Services to Start and Stop
+   - Activate and Deactivate Services for a Runlevel
+   - Activate and Deactivate Services for a Runlevel with YaST