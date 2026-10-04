# Taking Stock of Fedora Core System Configuration Files 407

### Table 1-3 Some Fedora Core Configuration Files
| Configuration File | Description |
| --- | --- |
| /boot/System.map | Map of the Linux kernel (maps kernel addresses to names of functions and variables) |
| /boot/vmlinuz | The Linux kernel (the operating system's core) |
| /etc/at.allow | Usernames of users allowed to use the at to schedule jobs for later execution |
| /etc/at.deny | Usernames of users forbidden to use the at command |
| /etc/bashrc | Systemwide functions and aliases for the BASH shell |
| /etc/cups/cupsd.conf | Printer configuration file for the Common UNIX Printing System (CUPS) scheduler |
| /etc/fonts | Directory with font files |
| /etc/fstab | Information about file systems available for mounting |
| /etc/group | Information about groups |
| /etc/grub.conf | Configuration for the Grand Unified Bootloader (GRUB) — the default boot loader in Fedora Core (this is a symbolic link to /boot/grub/grub.conf) |
| /etc/hosts | List of IP numbers and their corresponding hostnames |
| /etc/hosts.allow | Hosts allowed to access Internet services on this system |
| /etc/hosts.deny | Hosts forbidden to access Internet services on this system |
| /etc/httpd/httpd.conf | Configuration file for the Apache Web server conf |
| /etc/init.d | Directory with scripts to start and stop many servers |
| /etc/initab | Configuration file used by the init process that starts all the other processes |
| /etc/issue | File containing a message to be printed before displaying the text-mode login prompt (usually the Fedora Core version number) |
| /etc/lilo.conf | The configuration for the Linux LILO — one of the loaders that load the operating system from disk (present only if you use the LILO boot loader) |
| /etc/login.defs | Default information for creating user accounts, used by the useradd command |
| /etc/modprobe.conf | Configuration file with directives for loading kernel modules (for example, Ethernet and sound drivers) |
| /etc/mtab | Information about currently mounted file systems |

(continued)