+   * Shutdown immediately: sudo shutdown now
+   * Reboot: sudo shutdown -r now
+   * Schedule a shutdown: sudo shutdown +30 "System will shutdown in 30 minutes"

+   3. **reboot**: Reboot the system
+      
+      * sudo reboot

+   4. **poweroff**: Power off the system
+      
+      * sudo poweroff

+   5. **journalctl**: View systemd logs
+      
+      * View all logs: journalctl
+      * View logs for a specific service: journalctl -u service_name
+      * View kernel messages: journalctl -k

Understanding the system startup and shutdown processes, along with the tools to control them, is essential for effective system administration and troubleshooting in Debian.

# # Using Debian's Package Management System (APT)

Debian's Advanced Package Tool (APT) is a powerful package management system that simplifies the process of installing, updating, and removing software packages. APT handles dependencies, configuration, and upgrades, making system maintenance more efficient.

# ## APT Components

+   1. **apt**: High-level command-line interface for package management.
+   2. **apt-get**: Lower-level package management tool.
+   3. **apt-cache**: Query the APT package cache.
+   4. **dpkg**: Debian package manager (used by APT).