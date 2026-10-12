
unauthorized access to the boot settings, so click the check box, which will bring up the password box as shown.

![](img/ec2066d370d3af1a767664d36aa7ddfe_63_0.png)

The check box in the last section of the boot loader configuration screen allows you to set somewhat more esoteric features of the boot loader. If you check the box and click Next, you will get an advanced configuration screen (see Figure 2-11).

GRUB sets up on the master boot record (MBR) or the first partition on which Linux resides. The MBR is the very first thing the system will read when booting a system. It is essentially the point where the built-in hardware tests finish and pass off control to the software. This is the default; if you allow GRUB to be installed here, its graphical boot menu will load when you power on or reboot your system, and it will allow you to select which operating system to load. In a server configuration, there may be choices of Linux kernels to load, but there should just be one operating system option!

**NOTE**

SMP-based systems will start with two boot image choices. The first choice, Red Hat Linux, is set up to support multiple processors. In the event that you encounter a problem with this configuration, Red Hat Linux-up will also be available; it will utilize only one processor, but at least it will get you up and going.

If you are already using another boot loader and prefer it, then you will want to place GRUB on the first sector of the root partition. This will allow your preferred boot loader to run first and then pass control off to GRUB, should you decide to start Linux. Figuring out how to notify your preferred boot loader that there’s a new operating system available is up to you.

This screen also has an option to Force LBA32, which uses linear mode. This applies only to some SCSI drives or drives that are accessed in LBA mode, so unless you know that it applies to you, or are experimenting, leave the box unchecked.

The last option on this advanced configuration screen is a box that allows you to enter kernel parameters to be used at boot time. Most people can ignore this box. If the documentation for a particular feature or device requires you to pass a parameter here, add it; otherwise, leave it blank.

## Setting Up Networking

Now Red Hat is ready to configure your network interface cards (see Figure 2-12).

Each interface card recognized by Linux will be listed in the table at the top of your screen. Ethernet devices are listed as eth0, eth1, eth2, and so on. You can select each interface and click Edit to configure it using DHCP or to set the IP address by hand, as shown.

![](img/ec2066d370d3af1a767664d36aa7ddfe_64_0.png)

![](img/ec2066d370d3af1a767664d36aa7ddfe_65_0.png)

**Figure 2-12** Configure network cards and IP settings.

If you choose to configure by hand, be sure to have the IP and netmask values handy.

Check the Activate On Boot button for a card if you want the interface to be enabled at boot time.

On the bottom half of the screen, you’ll see the configuration choices for giving the machine a host name, a gateway, and related DNS information. If you have enabled DHCP on one of the network interfaces, you can opt to have the machine’s name set from the DHCP server.

> **NOTE**
>
> Even if you are not part of a network, you can fill in the host name. If you don’t fill in a host name, your computer will be known as localhost.

Once you have all of this filled in, simply click Next to continue.

## Firewall Configuration

The next screen allows you to configure the firewall functionality of your Linux system (see Figure 2-13).

![](img/ec2066d370d3af1a767664d36aa7ddfe_66_0.png)

**Figure 2-13** Configure the firewall properties on the Linux server.

How tightly or loosely you set access to the system will depend entirely on what type of function the server will perform. For example, if you want your system to serve as an NFS server so that other systems can mount its drives, you cannot set the high or medium security levels on this page. On the other hand, if you want this system to act as a web server without RealAudio content, the High security level may be the best choice.

If you don’t plan to have access to the console of your Linux server, you should be sure to allow a method of managing the system remotely; enabling SSH can do this. You’ll spend more time on configuring Red Hat Linux 8.0 to be secure in Module 9.

> **TIP**
>
> If it turns out you have over-constrained your server and are having problems accessing it or using it the way you intended, you can temporarily shut off the firewall using the command `/sbin/service iptables stop`, but be careful about doing so on a vulnerable network.

When you have configured the firewall properties to your Linux satisfaction, click Next to continue installation.

## Additional Language Support

If you wish to add support for languages in addition to the one you specified for the installation process, the next screen allows you to do so (see Figure 2-14). You can set up your Linux server as a virtual Tower of Babel if you do so choose.

Click Next after choosing all the additional languages you need.

## Time Zone Configuration

The time zone configuration screen (see Figure 2-15) allows you to select in which time zone the machine is located. If your system’s hardware clock keeps time in UTC, be sure to click the System Clock Uses UTC button so that Linux can determine the difference between the two and display the correct local time.

## Creating Accounts

The Red Hat Installation tool creates one account for you called *root*. This user account is similar in nature to the Administrator account under Windows 2000 and Windows .NET Server: The user who is allowed access to this account has full control of the system.

Thus, it is crucial that you protect this account with a good password. Be sure not to pick dictionary words or names as passwords, as they are easy to guess and crack.

![](img/ec2066d370d3af1a767664d36aa7ddfe_67_0.png)

![](img/ec2066d370d3af1a767664d36aa7ddfe_68_0.png)

**Figure 2-15** Select the correct time zone from the map or the text listing.

Part of protecting **root** means not allowing users to log in as the root user over the network. This keeps crackers from being able to guess your root password by using automated login scripts. In order to allow legitimate users to become the root user, you need to log in as yourself, and then use the **su** (switch user) command. Thus, setting the root password isn't enough if you intend to perform remote administration; you will need to set up a real user, as well.

In general, it is considered a good idea to set up a normal user to do day-to-day work anyway. This gives you the protection of not being able to accidentally break configuration files or other important components while you're just surfing the Net or performing nonadministrative tasks. The exception to this rule is, of course, certain server configurations where there should never be any users besides the root user (for example, firewalls).

In Figure 2-16, you see the screen that lets you set the root password as well as create new users.

Begin by picking a root password and entering it into the **Root Password** box at the top of the screen. Enter it again in the **Confirm box** right below; this protects you from locking yourself out of the system in case you make a typo. The text **Root Password Accepted** will appear below the password boxes once you have entered a password twice the same way.

44 Module 2: Installing Linux in a Server Configuration

![](img/ec2066d370d3af1a767664d36aa7ddfe_69_0.png)

**Figure 2-16** Set a strong password for the root user and add additional users.

You do not need to add the root user.

The remainder of the screen is meant for creating new user accounts. To do so, simply click Add to bring up the Add A User Account window as shown.

![](img/ec2066d370d3af1a767664d36aa7ddfe_69_1.png)
