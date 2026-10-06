# Daemon Used For By Function (Continued)

comsat | Notifies users of new mail | Used by biff, a utility that notifies users of incoming mail. If the user is logged on and has run biff y, comsat sends a message to the user's shell, saying that there is new mail (at an appropriate time). Security-conscious sites may want to disable this service, as it has a history of security holes. Launched by xinetd.

crond | cron | Used for periodic execution of tasks, this daemon looks in the /var/sp/cron/ directory for files that correspond to user's login names. It also looks at the /etc/crontab and files in the /etc/cron d. When a task comes for execution, crond executes it as the user who owns the file that describes task.

dhcpd | DHCP | Client daemon. Refer to "DHCP Client" on page 1028.

dhcpd | DHCP | Assigns Internet address, subnet mask, default gateway, DNS, and other information to hosts. This protocol answers DHCP requests and, option-alBOOT requests. See DHCP on page 1465.

fingerd | finger | Handles requests for user information from the finger utility. Launched by xinetd.

ftpd | FTP | Handles FTP requests. Refer to "ftp: Transfers Files over a Network" on page 378. Launched by xinetd.

gpm | General-purpose mouse or GNU state manager | Allows you to use a mouse to cut and paste text on console applications.

httpd | HTTP | A Web server daemon. See HTTP on page 1472.

inetd | | Deprecated in favor of xinetd.

lpd | line printer spooler daemon | Launched by xinetd when printing requests come to the machine.

named | DNS | Supports DNS (page 1465), which has replaced the use of the /etc/hosts file for hostname-to-IP address mapping on most networked UNIX/Linux systems.

nfsd, statd, lock, mount, rquota | NFS | These five daemons operate together to handle NFS (page 1482) operations. The nfsd daemon handles file and directory requests. The statd and lock daemons implement network file and record locking. The mount daemon takes care of converting a filesystem name request from the mount utility into an NFS handle and checks access permissions. Finally, if disk quotas are enabled, rquota handles those.