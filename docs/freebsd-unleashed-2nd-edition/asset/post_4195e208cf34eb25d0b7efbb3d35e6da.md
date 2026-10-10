
![](img/48eec858cce7dfb89da36a4d40b7daf3_835_0.png)

**FIGURE 34.3** The main dhcpcconf menu.

Note that the mouse cannot be used in this program. You will need to use the arrow keys, the Enter key, and the Tab key to navigate in the program.

The first menu option (**Common**) sets options that apply to all IP addresses assigned. This is the default configuration information that will be sent to clients. Press Enter to select it. Figure 34.4 shows the Common dialog.

![](img/48eec858cce7dfb89da36a4d40b7daf3_835_1.png)

**FIGURE 34.4** Here you set options common to all IP addresses, as well as default options.

Most of the options listed here are self-explanatory, with the exception of the first one, which defines the minimum and maximum lease periods.

The *minimum* lease is also the default lease period. This is the default time in seconds that a lease will be good for. The *maximum* time is the maximum amount of time that the server will lease an IP address. The client can request a longer lease than the default defined in minimum, but the server will never lease an IP for longer than the value defined in maximum.

The default minimum lease period is **600** seconds (10 minutes), and the default maximum lease period is **7200** seconds (120 minutes). The client must renew its lease before the maximum lease period is up; otherwise, it will lose the lease, and the IP address it has will be placed back into the pool of available addresses.

Here are some considerations to think about if you want to change the default lease:

- Shorter lease times mean unused IP addresses will be placed back into the pool faster. What's more, configuration changes will be recognized faster. However, if a lease expires on a client and that client attempts to connect to the network when the DHCP server is unavailable, the client will not be able to use any network resources until the DHCP server comes back online.
- Longer lease times help protect against DHCP server outages. If the DHCP server is down, a client can still connect to the network as long as it has a valid lease on an IP address. However, configuration changes will not be recognized as quickly, and unused IP addresses will be tied up longer.

Once you have filled in all the values here, tab to the <Keep> button and press Enter. This will take you back to the main screen.

## Configuring Fixed-Host Entries

In some situations, you might need to reserve static IP addresses (IP addresses that never change) for some systems, such as for systems that are acting as servers. This arrangement is called a *fixed host*. The second option, DHCP Configurator, allows you to reserve static addresses. Figure 34.5 shows the Fixed-Host Entries configuration dialog.

![](img/48eec858cce7dfb89da36a4d40b7daf3_836_0.png)

**FIGURE 34.5** Configuring information for systems that require static IP addresses.

Table 34.3 shows the options in this dialog and what they do.

**TABLE 34.3 Fixed-Host Configuration Options**

| Option | Description |
| :--- | :--- |
| New entry hostname | This is the hostname of the system that is being configured for static IP. You should provide only the hostname here, not the domain name, because the domain information was provided in the Common options. |
| New entry HW address | Enter the hardware address of the network card on the host that is being configured for static IP here. |
| New entry IP address | This is the static IP address that the host being configured for static IP will use. |

Once you have finished entering the information, in the last field, press Enter to add the host to the list. You can then enter more hosts if you want, or you can tab down to `<Keep>` to return to the main menu. Note that you must press Enter after filling in the last entry. If you do not, and you simply tab to `<Keep>`, the entry will be lost.

## Configuring Subnet Ranges

Finally, you need to configure the IP address ranges that are available on various subnets. Select the Subnet option from the main menu to do this. Figure 34.6 shows the Subnet configuration dialog.

![](img/48eec858cce7dfb89da36a4d40b7daf3_837_0.png)

Table 34.4 shows what these options do.

**TABLE 34.4 Subnet Range Options**

| Option | Description |
| :--- | :--- |
| New range subnet | This is the subnet that this range of IP addresses will affect. |
| New range start IP | This is the first IP address that will be available to DHCP clients on this subnet that are receiving dynamic IP addresses. |
| New range end IP | This is the last IP address that will be available to DHCP clients on this subnet that are receiving dynamic IP addresses. |

As with the Fixed-Host Configuration dialog, you must press Enter here after entering the range end IP address for the entry to be added to the list and for the changes to take effect. After you have done so, you can add more entries if you want.

If you want to have multiple IP address blocks available to a single subnet, simply create a new entry for the same subnet as an existing entry and include a different IP address range. Both of the entries will be valid, and both of the ranges of IP addresses will be available to the subnet.

Once you have finished creating all the entries you want, tab to <Keep> and press Enter to return to the main menu.

> **TIP**
> If you are unclear about some of the networking terminology in this chapter, such as subnets, and so on, see Chapter 21, “Networking with FreeBSD,” for information on these various networking concepts.

## Saving the Information and Quitting

From the main menu of DHCP Configurator, tab to the <Save> button and press Enter. The program will create the configuration file and then exit. The configuration file will be located in /etc/dhcpd.conf.

# PART V

# X-Windows

# IN THIS PART

CHAPTER 35 Advanced X-Windows Configuration 809

# CHAPTER 35

# Advanced X-Windows Configuration

Chapter 4, “Your First Session with FreeBSD,” Chapter 5, “Working with X-Windows,” and Chapter 6, “Working with Applications,” discussed some basics of the X-Windows system. X-Windows is a very powerful server framework, however, that can do much more than provide a basic desktop functionality. Other capabilities of X-Windows include the ability to display the output of graphical applications over a network. This chapter looks at these and other advanced features of X-Windows, starting with advanced configuration information of the basic X-Windows system.

## Configuring X-Windows with the xf86config Script

The xf86config tool will ask you a series of questions and configure X-Windows based on the answers you provide.

> **CAUTION**
> Improper use of this tool when configuring video settings could actually cause physical damage to your hardware. Although most monitors have built-in protection circuits these days and will shut themselves down if you try to drive them with a refresh rate higher than they support, some monitors will try to display the screen at the given refresh rate, even if the monitor’s hardware is not capable of handling it. The result could destroy your monitor.

# IN THIS CHAPTER

- Configuring X-Windows with the xf86config Script
- Understanding the XF86Config File
- Testing the X-Windows Setup
- Your Personal .xinitrc File
- Working with Fonts
- Using Remote X-Windows Clients
- Using the xdm Graphical Login Manager

> **CAUTION**
> The xf86config program will overwrite your existing XF86Config file. If you have a working XF86Config file and you want to experiment with a new configuration, you should back up your existing file first. The file is located in `/etc/X11/XF86Config`. Make a copy of this file to `/etc/XF86Config.bak` (or some other name) before continuing. This way, you can restore your previous configuration easily if your new configuration does not work by simply copying the backup file back to `/etc/X11/XF86Config`.

You will need to be root to use this program. As the root user, type `xf86config` at the command prompt and press Enter. You will see a screen like the following:

This program will create a basic XF86Config file, based on menu selections you make.

The XF86Config file usually resides in `/usr/X11R6/etc/X11` or `/etc/X11`. A sample XF86Config file is supplied with XFree86; it is configured for a standard VGA card and monitor with 640x480 resolution. This program will ask for a pathname when it is ready to write the file.

You can either take the sample XF86Config as a base and edit it for your configuration, or let this program produce a base XF86Config file for your configuration and fine-tune it.

Before continuing with this program, make sure you know what video card you have, and preferably also the chipset it uses and the amount of video memory on your video card. SuperProbe may be able to help with this.

Press enter to continue, or ctrl-c to abort.

Once you have read the information, simply press Enter to continue. The first thing you will be asked to configure is your mouse.

> **CAUTION**
> Double-check your typing when entering values in xf86config. The program is not very forgiving of mistakes and typos. If you accidentally make a wrong entry and don't catch it before you have pressed Enter, there is no way to back up and fix it. You will have to press Ctrl+C to exit the program and then start completely over again.
