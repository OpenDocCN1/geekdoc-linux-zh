```
drwxr-xr-x 2 root root 1024 Jul 18 18:07 rc3.d
drwxr-xr-x 2 root root 1024 May 27 1995 rc4.d
drwxr-xr-x 2 root root 1024 Jul 6 15:12 rc5.d
drwxr-xr-x 2 root root 1024 Jul 6 15:12 rc6.d
```

If you are trying to track down where your Ethernet interface and associated network routes are actually configured, you will need to track through these files to find where the commands are that do this.

# Distribution-Specific PPP Configuration Tools

On some installations (for example Red Hat and Caldera), there is a X Windows configured PPP dial-up system. This HOWTO does not cover these distribution-specific tools. If you are having problems with them, contact the distributors directly.

For Red Hat 4.x users, there is now a Red Hat PPP-TIP (see http://www.interweft.com.au) in the Linux resources area and also from Red Hat Software (see http://www.redhat.com) in the support area.

# IP NUMBERS

Every device that connects to the Internet must have its own, unique IP number. These are assigned centrally by a designated authority for each country.

If you are connecting a local area network (LAN) to the Internet, you must use an IP number from your own assigned network range for all the computers and devices you have on your LAN. You must not pick IP numbers out of the air and use these while connecting to another LAN (let alone the Internet). At worst this will simply not work at all and could cause total havoc as your "stolen" IP number starts interfering with the communications of another computer that is already using the IP number you have picked out of the air.

Please note that the IP numbers used throughout this document (with some exceptions) are from the "unconnected network numbers" series that are reserved for use by networks that are not (ever) connected to the Internet.

There are IP numbers that are specifically dedicated to LANs that do not connect to the Internet. The IP number sequences are

+   * One A Class Network Address 10.0.0.0 (netmask 255.0.0.0)

![](bbox=[0.87, 0.52, 0.99, 0.63])