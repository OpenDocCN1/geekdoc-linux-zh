**Table 1-3 (continued)**
| Path | Description |
| --- | --- |
| `/etc/passwd` | Information about all user accounts (actual passwords are stored in `/etc/shadow`) |
| `/etc/profile` | Systemwide environment and startup file for the BASH shell |
| `/etc/rc.d` | Directory that holds startup and shutdown scripts for the Fedora Core system |
| `/etc/rc.d/rc.sysinit` | Fedora Core initialization script |
| `/etc/shadow` | Secure file with encrypted passwords for all user accounts (can be read only by root) |
| `/etc/shells` | List of all the shells on the system that the user can use |
| `/etc/skel` | Directory that holds initial versions of files such as `.bash_profile` that copy to a new user’s home directory |
| `/etc/sysconfig` | Fedora Core configuration files |
| `/etc/sysctl.conf` | Configuration file with kernel parameters that are read in and set by `sysctl` at system startup |
| `/etc/termcap` | Database of terminal capabilities and options |
| `/etc/udev` | Directory containing configuration files for `udev` — the program that provides the ability to dynamically name hot-pluggable devices and create device files in the `/dev` directory |
| `/etc/X11/xorg.xof` | Configuration file for X.org X11 — the X Window System |
| `/etc/X11/gdm` | Directory with configuration files for the GDMOE display manager (gdm) |
| `/etc/xinetd.conf` | Configuration for the `xinetd` daemon that starts a number of Internet services on demand |
| `/etc/yum.conf` | Configuration for the `yum` package updater and installer |
| `/var/log/cron` | Log file with messages from the `cron` process that runs scheduled jobs |
| `/var/log/httpd/access_log` | Web-server access log |
| `/var/log/httpd/error_log` | Web-server error log |
| `/var/log/messages` | System log |

# Monitoring System Performance

When you’re the system administrator, you must keep an eye on how well your Fedora Core system is performing. You can monitor the overall performance of your system by looking at information such as