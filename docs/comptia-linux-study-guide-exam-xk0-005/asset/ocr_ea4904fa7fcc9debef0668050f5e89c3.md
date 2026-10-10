+   16. A customer has complained that a service on your SysV init system is not working. Which of the following commands is the best command to use to check the service?
+   A. `service start`
+   B. `service status`
+   C. `service --status-all`
+   D. `service stop`
+   E. `service reload`

+   17. You need to enable the DHCP service on your Red Hat-based SysV init system for runlevels 3 and 5. Which of the following commands should you use?
+   A. `service enable dhcp 3,5`
+   B. `chkconfig --levels 3,5 dhcp on`
+   C. `chkconfig --levels 35 on dhcp`
+   D. `chkconfig --levels 35 dhcp on`
+   E. `service enable dhcp 35`

+   18. You need to enable the DHCP service on your Debian-based SysV init system for the default runlevels. Which of the following commands should you use?
+   A. `update-rc.d dhcp default`
+   B. `chkconfig --default dhcp on`
+   C. `update-rc.d default dhcp`
+   D. `update-rc.d defaults dhcp`
+   E. `update-rc.d dhcp defaults`

+   19. Which of the following would be the appropriate base name for a mount unit file that mounts a filesystem at the `/var/log/` mount point?
+   A. `/var/log.mount`
+   B. `/var/log.unit`
+   C. `var-log.mount`
+   D. `var-log.unit`
+   E. `var/log.mount`

+   20. You are managing a systemd system and need to create an automount unit file. Which of the following directives should you review to possibly include in this file's [Autounit] section? (Choose all that apply.)
+   A. `Where`
+   B. `Options`
+   C. `DirectoryMode`
+   D. `TimeOutIdleSec`
+   E. `What`