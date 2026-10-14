/usr/sbin/named were in enforce mode and I had commented out the line in the /usr/sbin/named profile that granted read access to /etc/bind/**, then reloaded AppArmor and restarted BIND, not only would BIND not start (since it couldn’t read its config files), I would get a nice log entry in /var/log/syslog from the kernel to report the denied attempt:

```
Jan  7 19:03:02 kickseed kernel: [ 2311.120236]
audit(123138782.081:3): type=1503 operation="inode_permission"
requested_mask="::r" denied_mask="::r" name="/etc/bind/named.conf"
pid=5225 profile="/usr/sbin/named" namespace="default"
```

# Ubuntu AppArmor Conventions

+   - **/etc/apparmor/**  
+     This directory contains the main configuration files for the AppArmor program, but note that it does *not* contain AppArmor rules.
+   - **/etc/apparmor.d/**  
+     You will find all of the AppArmor rules under this directory along with subdirectories that contain different sets of include files to which certain rule sets refer.
+   - **/etc/init.d/apparmor**  
+     This is the AppArmor init script. By default AppArmor is enabled.
+   - **/var/log/apparmor/**  
+     AppArmor stores its logs under this directory.
+   - **/var/log/syslog**  
+     When an AppArmor rule is violated in either enforce or complain mode, the kernel generates a log entry under the standard system log.

# SSH Security

If you are going to run services on your servers, these days it’s a safe bet that one of them will be SSH. SSH provides a secure, encrypted channel between your desktop and a server so that you can run commands and manage the machine without having to physically be there with a keyboard