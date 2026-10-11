+   - Set up of LVM
+   
+   - Delete unnecessary files in /var/lock/
+   
+   - Set the system time
+   
+   - Configure PnP hardware with the isapnp tools

**boot.local**. This script includes additional commands to execute at boot before changing into a runlevel. You can add your own system extensions to this script.

**halt**. This script is run if runlevel 0 or 6 is entered. It is called up either with the command halt (the system is completely shut down) or with the command reboot (the system is shut down and then rebooted).

**rc**. This script is responsible for the correct change from one runlevel to another. It runs the stop scripts for the current runlevel, and then it runs the start scripts for the new one.

**service**. Each service (like cron, apache2, cups) comes with a script allowing you to start and stop the service, to reload its configuration, or to view its status. To create your own scripts, you can use the file /etc/init.d/skeleton as a template.

# Runlevel Symbolic Links

To enter a certain runlevel, init calls the script /etc/init.d/rc with the runlevel as parameter. This script examines the respective runlevel directory /etc/init.d/rc*.d/ and starts and stops services depending on the links in this directory.

For each runlevel, there is a corresponding subdirectory in /etc/init.d/. For runlevel 1 it is /etc/init.d/rc1.d/, for runlevel 2 it is /etc/init.d/rc2.d/, and so on.