
## Chapter 21: Network Configuration and Security

## Installing and Configuring a Firewall

As mentioned in the previous section, many different software packages are available to help you configure and activate a firewall on your Ubuntu system. These packages include the default package that is installed on Ubuntu systems, ufw (the Uncomplicated Firewall), Lokkit, Firestarter, Fwbuilder, Guardguard, and many more.

The default firewall package for Ubuntu systems, ufw, is relatively easy to configure from the command line, but is even easier to configure using its associated graphical configuration utility, gufw. Unfortunately, this utility is not installed by default on Ubuntu systems. You will have to install it using your favorite Package Management tool, as discussed in Chapter 19. This graphical configuration tool is worth using unless you're a firewall wizard (in which case, I doubt you'd be reading this section) and therefore the rest of this section focuses on using the graphical gufw utility.

Installing the gufw graphical configuration utility adds the Firewall Configuration menu entry to the System Administration menu on an Ubuntu system. Select this menu entry to begin configuring your firewall. After entering your password, the initial gufw dialog appears, as shown in Figure 21-13.

FIGURE 21-13
The initial gufw dialog

![](img/1a233c34336fbf5a85d6eb785e401709_832_0.png)

The first thing you will want to do when configuring a firewall is to enable that firewall on your system. Click the "Firewall enabled" checkbox to do so. The shield graphic shown in Figure 21-13 will be displayed in green, helping you identify the fact that the firewall is now enabled and that your system is secure if you use the current configuration. The other configuration options on the gufw dialog will also be enabled, as shown in Figure 21-14.

Enabling your firewall

![](img/1a233c34336fbf5a85d6eb785e401709_833_0.png)

The gufw tool's Add button displays a dialog that makes it easy for you to create various types of rules without having to understand the syntax of the kernel's iptables rules. Click Add to display this dialog. Once you enable a firewall, all incoming traffic is disabled by default, which is secure but probably not what you want if you plan to support network services such as incoming connections, including FTP, and so on. Note that you do not need to select the "Allow incoming" radio button shown in Figure 21-14 to enable incoming traffic. The radio buttons at the top left of the gufw dialog identify the default behavior of your system. Any rules that subsequently represent exceptions to that rule. For example, to quickly create a rule that allows incoming SSH connections, make sure that the Simple tab is selected in the "Add rule" dialog, enter ssh in the entry field for this rule, and make sure that the first two fields display "Allow" and "In", respectively, as shown in Figure 21-15. Click Add to add the new rule. Once you add a rule, it displays in the main gufw dialog.

Click Add to add the new rule. The rule is added to the list of rules shown in the bottom of the gufw dialog, as shown in Figure 21-16, and your firewall will now allow both incoming and outbound SSH traffic.

## FIGURE 21-15
Allowing inbound/outbound SSH connections through your firewall

![](img/1a233c34336fbf5a85d6eb785e401709_834_0.png)

## FIGURE 21-16
Rules for allowing inbound SSH connections

![](img/1a233c34336fbf5a85d6eb785e401709_834_1.png)

The rules shown at the bottom of the gufw rules dialog refer to the ports associated with various services, which is not very user-friendly. If you aren't sure about the service that a rule is associated with, you can use the grep command to look up the port that it uses in the file /etc/services. For example, the following output shows how to look for the services associated with port 22 in this file:

```
$ grep -w 22 /etc/services
ssh 22/tcp # SSH Remote Login Protocol
ssh 22/udp
```

The other tabs in gufw utility rule dialog make it easy to define other types of rules. The Preconfigured tab provides a drop-down menu with number of default rules that you can use to enable (or disable) external access to various programs and services. To create a rule associated with a service rather than a specific program, click Programs, and select Services from the drop-down menu that displays. You can then click the fourth field to display a list of services for which pre-defined rules exist, as shown in Figure 21-17.

FIGURE 21-17
Preconfigured rules for various services

![](img/1a233c34336fbf5a85d6eb785e401709_835_0.png)

You can also use the Preconfigured tab to define other types of rules by selecting them from the Type dropdown menu at the left. For example, Figure 21-18 shows a rule that enables NFS traffic but also limits the bandwidth by that service.

If you need more complex rules than the ones that can be created from the Simple or Preconfigured tabs, the Advanced tab, shown in Figure 21-19, provides a general mechanism for defining more sophisticated rules.

FIGURE 21-18
Enabling NFS access

![](img/1a233c34336fbf5a85d6eb785e401709_835_1.png)

Defining advanced rules

![](img/1a233c34336fbf5a85d6eb785e401709_836_0.png)

The Advanced Rules tab makes it easy for you to add host or network-specific rules that enable traffic from specific hosts or networks to specific ports on your system, and vice versa.

Once you have finished defining the rules for the traffic that your firewall will allow or deny, click Close to save your rules and terminate the gufw utility. If you're curious, you can use the sudo iptables -L command to see the rules that you have just created look like, which should make you eternally grateful for a tool like gufw.

## Summary

This chapter explained the basics of setting up wired and wireless network connections on your Ubuntu system. Ubuntu systems provide easy-to-use graphical applets that simplify configuring these types of interfaces, eliminating the traditional command-line magic required when you are using the ifconfig command. This chapter also provided a basic discussion of securing your Ubuntu system and related networking hardware, and also discussed up a simple firewall on your Ubuntu system.

Chapter 22 discusses using wireless technologies on your Ubuntu system in more detail, providing a detailed explanation of setting up and using WiFi, an alternative to the Network Manager software that was discussed in this section. Chapter 22 also includes a detailed explanation of how to use Windows drivers on your Ubuntu system to make new or problematic Ethernet and other devices work with your new Linux system.

## Going Wireless

Today's mandatory connectivity requirements would be a farce throughout the ubiquity of wireless connections, whether these are cell phones leveraging a distant tower, your cell phone or PDA syncing to your PC via Bluetooth or infrared, or your laptop using wireless network connections via an access point hidden in the linen closet in your hotel. It is incredibly liberating to travel without carrying every cable and adapter that could possibly connect device A to device B, especially when airport security seems to frown on suitcases full of cables, power supplies, and hardware (no relation to the author as seen in the laboratory of Victor von Frankenstein)

Like many other high-tech domains, wireless networking has its own vocabulary and a bewildering set of alphabetically similar but arguably unique acronyms; protocols, and so on. The first section of this chapter provides a basic overview of wireless networking and terminology today. Subsequent sections of this chapter explain how to configure wireless devices that are directly supported by Linux, explain how to work with wireless devices that are not supported by Linux (an impressive trick), and provide tips and tricks for using Microsoft Windows drivers with your Ubuntu Linux system.

# THIS CHAPTER

-   Understanding wireless networking terminology
-   Installing and using Wcid
-   Using Windows drivers
-   Troubleshooting Windows drivers

# Overview of Wireless Technologies

Wireless networking is amazingly useful, both on the job (so that you never have to play rock/paper/scissors over a limited number of Ethernet cables in a conference room) and even more when traveling, enabling you to
