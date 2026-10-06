# Table 4-1 (continued)

| File | Description |
| --- | --- |
| modules.conf | Contains aliases and options related to loadable kernel modules used by your computer. |
| mtab | Contains a list of file systems that are currently mounted. |
| mtools.conf | Contains settings used by DOS tools in Linux. |
| named.conf | Contains DNS settings if you are running your own DNS server. |
| ntp.conf | Includes information needed to run the Network Time Protocol (NTP). |
| passwd | Stores account information for all valid users of the system. Also includes other information, such as the home directory and default shell (Rarely includes the user passwords themselves, which are typically stored in the `/etc/shadow` file). |
| printcap | Contains definitions for the printers configured for your computer. (If the `printcap` file does not exist, look for printer information in the `/etc/cups` directory). |
| profile | Defines system-environment and startup programs for all users. This is read when the user logs in. |
| protocols | Sets protocol numbers and names for a variety of Internet services. |
| resolv.conf | Identifies the locations of DNS name servers that are used by TCP/IP to translate Internet hostnames into IP addresses. (When a browser or mail client requests an Internet site, it checks servers in this file to locate the site). |
| rpc | Defines procedure call call names. |
| services | Defines TCP/IP services and their port assignments. |
| shadow | Contains encrypted passwords for users who are defined in the `passwd` file. (This is a more secure way to store passwords than the original encrypted password in the `passwd` file. The `passwd` file needs to be publicly readable, whereas the `shadow` file can be unreadable by all but the root user). |
| shells | Lists the command-line interpreters (`bash`, `sh`, `csh`, and so on) that are available on the system, as well as their locations. |
| sudoers | Sets commands that can be run by users, who may not have permission to run the command, using the `sudo` command. In particular, this file is used to provide selected users with root permission. |
| syslog.conf | Defines what logging messages are gathered by the `syslog` daemon and what files they are stored in. (Typically, log messages are stored in files in the `/var/log` directory).