# TABLE 15.1

# SYSTEM IDENTIFICATION INFORMATION

| Information Required | Command(s) Used to Gather the Information |
|---|---|
| System name | /usr/bin/uname -u |
| Primary network interface | ifconfig -a |
| IP address | ypmatch <system_name>
<host>nismatch <system_name>
more /etc/inet/hosts |
| Domain name | /usr/bin/domainname |
| Whether part of a subnet | more /etc/netmasks |
| What name service is used | more /etc/nsswitch.conf |

Next, verify that you have enough disk space for Solaris 8 and all the copackaged and third-party software you plan to add. (Refer to Chapter 3 for the total size of each software configuration cluster.) Normally, a server would have several gigabytes (GB) of disk space available for the operating system, so you'll be installing the full distribution cluster. Also, you need to check with your software vendor regarding space requirements for any third-party software packages as well as swap space requirements.

In addition, make sure you have enough disk space if you plan to run the following software:

+   - AnswerBook2
- Desktop Power Pack
- Internet Mail Service
- ODBC Driver Manager
- OpenGL
- Solstice AdminSuite
- Solstice Backup
- Solstice DiskSuite
- Solaris 8 Documentation
- Sun Hardware AnswerBook