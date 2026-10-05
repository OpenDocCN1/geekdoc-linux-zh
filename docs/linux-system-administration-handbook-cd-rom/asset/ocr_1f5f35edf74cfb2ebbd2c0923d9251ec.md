# C.2 Upgrading from Existing Caldera or Linux Systems

| Table C-1 | Files you may want to copy before installing your new system |
|---|-|
| If you want to preserve this | Copy this file or directory |
| X Windows configuration | /etc/Xaccel.ini or /etc/XF86config |
| Boot manager configuration parameters (such as boot parameters to recognize hardware) | /etc/lilo.conf |
| IP networking information (such as, hosts, nameserver, and domain name) | /etc/hosts and /etc/resolv.conf |
| Filesystems mounted on your system | /etc/fstab |
| Names and passwords of all users on your system | /etc/passwd and /etc/group |
| Any home directories for users on system | /home |
| Any of your user settings | /usr |

# Adding Caldera's Commercial Packages to Other Linux Distributions

You can upgrade to OpenLinux from another Linux distribution. Many users have successfully installed Caldera's commercial packages on other ELF-based Linux 2.x systems. However, before upgrading, you should know Caldera does not provide support for other Linux systems and the upgrade instructions provided here may not work on your system.