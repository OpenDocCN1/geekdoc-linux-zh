
![](img/cae5c706c216875d12d4b7d28144cc71_52_0.png)

Figure 2.8 LILO configuration—boot options.

## Step 7. Installing and Configuring LILO

The first LILO configuration screen (Figure 2.8) will appear and will ask about the use of linear mode. As it clearly says, it pertains to SCSI drives only—and we will address this issue in our SCSI installation after this section. On older versions of the Red Hat distribution, it did not state that it was specific to SCSI installations. If you were to choose to enable this feature, it would have no effect—nor would it cause any problems. We choose to remove the default \* on Use linear mode . . . .

We plan to use LILO to manage the disk (see Figure 2.9). Therefore, we are going to choose the Master Boot Record (MBR) option. If there were some other alternate operating system partitions on the disk, the Linux configuration program would see them and you could choose to add them to your /etc/lilo.conf file as boot choices (see Figure 2.10). Because we are only installing the one Linux system, we will let this choice default to booting Linux. If your system is a production system, we recommend that no other operating systems should share the disk. This situation will primarily simplify the maintenance, backup, and recovery of the system. In other working environments, however, such as at home, you might appreciate having more than one operating system from which to choose.

## Step 8. Network Configuration

We are going to use a static IP address in the screen shown in Figure 2.11. But, if this system is going to be a print server or will run any services for other hosts, it should receive its own static IP address so that it will not

![](img/cae5c706c216875d12d4b7d28144cc71_53_0.png)

![](img/cae5c706c216875d12d4b7d28144cc71_53_1.png)

change. If the address changes, then other hosts on the network might not be capable of finding the service. Another issue to examine is whether any software on this host is not sensitive to having the IP address changed. Because we knew this machine would join an existing network and would eventually access the Internet, the IP addressing information we provided was as follows:

- Disable bootp/dhcp
- IP address: 192.168.2.205
- Netmask: 255.255.255.0

![](img/cae5c706c216875d12d4b7d28144cc71_54_0.png)

**Figure 9.21** Network configuration.

- Default gateway: 192.168.1.1
- Primary nameserver: 24.64.2.33
- Secondary nameserver: 24.64.2.34

You can revisit this menu at any time after the installation via the `/usr/sbin/netconf` or `/usr/sbin/netcfg` utilities. Please note that there is no opportunity during the installation to configure an ISP Internet connection. You can configure this option after the installation by using the `/usr/sbin/internet-config` utility.

## Step 9. Firewall Configuration

Firewall configuration (see Figure 2.12) is a new feature added to the Red Hat 7.1 distribution. This feature will not appear on the Red Hat 7.0 or previous equivalent distributions. This feature is a response to concerns that users had about security exposure on the Linux system itself. This particular feature set does *not* create a firewall appliance in the sense that this system can be used as a firewall for other systems. This feature set just provides some firewall protection to the system on which it is being installed. Now, about these Security Levels: For example, if you choose Medium as an option, it will prevent Telnet access *to* the system but will *not* prevent Telnet connections *through* the system if the system is now or eventually

![](img/cae5c706c216875d12d4b7d28144cc71_55_0.png)

equipped with two network cards, Linux can be used on firewalls, but this goal is not the objective of this dialog box.

Because in our shop we already have a proper firewall in place and we wish to have easy Telnet access to this system from various points on the network so that we can manage it remotely, we chose **No firewall**.

If the system you are installing Linux on is to be at the end of ISP service, we would recommend **Medium** or **High** so that it would not be as easy a target for hackers. Meanwhile, you can reconfigure this information after the installation via the `/usr/sbin/firewall -config` utility.

## Step 10. Mouse Selection

The system immediately asks you to configure the mouse if it senses one, as shown in Figure 2.13. If you have a three-button mouse, you will be better equipped to take advantage of the X Window system (please refer to Chapter 14, "The Linux X Window System") without confusion. For example, on a three-button mouse, the left button is copy; the middle button is paste; and the right button is used for context. On a two-button mouse, the left button is copy and the right button is paste. If you have a two-button mouse and you choose Emulate 3-buttons, then the left button will be copy, the right will be context, and clicking the left and right buttons together will be equivalent to the middle button. We have a two-button mouse. We chose Generic - 2 button Mouse (PS/2) and Emulate

![](img/cae5c706c216875d12d4b7d28144cc71_56_0.png)

Figure 2.13 Mouse selection.

three buttons. You can revisit this information after the installation via `/usr/sbin/mouseconfig`.

## Step 11. Language Support

We chose English (USA) in the screen shown in Figure 2.14 because we wish to have those code pages installed on this system. Installing more language support uses up significant space on your disk. All message files, code pages, and related files—such as screen fonts for the X Windows system—will be installed along with the language support.

If you are going to install additional or different language support here, give some thought to what you are going to use for keyboard support. Language support and keyboard support generally go hand in hand. This information can also be reconfigured after the installation via `/usr/sbin/locale_config`.

## Step 12. Time Zone Configuration

Somewhere in your hardware setup plan, way back at the beginning, should have been instructions to set the time properly in the system CMOS. Does your CMOS time function on your system handle Greenwich Mean Time (GMT)? If it does and you are going to use the system itself as a source of time, then set the time in the CMOS and use the hardware clock set to GMT option here. Then, it will convert the time set in your CMOS to

![](img/cae5c706c216875d12d4b7d28144cc71_57_0.png)

Figure 2.14 Language support.

the local time. If your CMOS date and time does not have the GMT capability and you set the time in your CMOS to the local time, then do not set the feature in the screen shown in Figure 2.15. The decision to use the hard-

![](img/cae5c706c216875d12d4b7d28144cc71_57_1.png)

Figure 2.15 Time zone selection.

ware clock will ultimately have to do with whether or not this system will be a standalone entity with respect to time. For example, standalone are often used by developers or by system administrators as utility systems. If the system is going to be a server, it might have to participate in a network by using the *Network Time Protocol* (NTP). Then, it would be appropriate to make use of the Time Zone Selection. Plan for this situation ahead of time. We cannot tell you how messed up a database server can get if the time is set in the past. Not many database applications can recover from time changes gracefully. We chose *not* to use the hardware clock because we have the local time set in our CMOS, but we did choose Canada/Mountain (a little local bias, eh?). This information can be reconfigured after the installation via /usr/sbin/timeconfig.

## Step 13. Root Password

Remember to choose a good password (see Figure 2.16) and then ensure that you remember it. Linux has rules and guidelines for proper passwords. Reviewing them would be worthwhile. Check the man pages (we discuss these manual pages for commands in Chapter 3, "Getting Started Using the Linux System") for passwd and the Red Hat online documentation for guidelines. This password can be reset after the installation by first logging in as *root* and using the *passwd* utility.

![](img/cae5c706c216875d12d4b7d28144cc71_58_0.png)

Specifying the root user password.
