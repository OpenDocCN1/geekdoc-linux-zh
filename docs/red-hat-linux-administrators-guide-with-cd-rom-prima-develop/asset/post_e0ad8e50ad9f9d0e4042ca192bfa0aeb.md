
![](img/a0884097af3186d9b4f616aaa3f065b0_535_0.png)

**FIGURE 15.4**
*Editing the primary Ethernet device.*

![](img/a0884097af3186d9b4f616aaa3f065b0_535_1.png)

**FIGURE 15.5**
*Setting up routing in the Network Configurator dialog box’s Routing tab.*

To connect to other hosts, you could add your alternate gateway’s IP address into this tab and create a static route to another network. Most Linux users will seldom use this tab, because most networks do not require a static route. If, however, you find yourself behind a firewall, as is frequently becoming the case on many networks, this tab can assist you in configuring your network settings.

## Running linuxconf for Networking

Another utility that provides added networking options is the linuxconf program. Its GUI is fast evolving into an all-purpose tool for editing most any text file found on the Linux system. You will find many features of the linuxconf utility that assist you in editing system configuration files on your Red Hat Linux system. There are too many features to look at in depth in this section, but carefully perusing and becoming familiar with the many features of linuxconf will help you understand your system even better. The linuxconf utility is constantly being updated and developed further to provide additional functionality.

The network tools for this utility are located within the first major section of the linuxconf tree structure called Config. For specifics regarding the basic host configuration options, look in the following directories: Config, Networking, Client tasks. The section detailing the different Config options is one of the first configurable items of the many sections listed in the tree-like structure. Figure 15.6 is a sample display in which a user can enter basic host networking information.

In the tree-structure file list, click Config, Networking, Client tasks, Basic host information. You can then configure not only the name of your system and its IP addresses but also any network devices. The current version of linuxconf displays four network devices by default, although you can override the default and specify that the utility display additional devices.

Additionally, the next entry within the Client tasks section, the Name server specification file or Resolver configuration file, displays all the name server information needed to allow your system to resolve DNS issues and to speak with other systems locally (see Figure 15.7).

![](img/a0884097af3186d9b4f616aaa3f065b0_536_0.png)

**FIGURE 15.6**
*The basic host configuration section under the Networking tools of linuxconf.*

![](img/a0884097af3186d9b4f616aaa3f065b0_537_0.png)

**FIGURE 15.7**

*The resolver configuration settings under the linuxconf program.*

The linuxconf utility offers several options that enable you to tailor the name servers and DNS search patterns just as easily as you could in the simple text file. For this task, some users consider using the GUI even easier than working with the text file. Beginning users should try both alternatives before deciding which one they prefer. Explore linuxconf’s two windows, such as the Host Name Search Path or the Name server access window as it is displayed in its dialog box as shown in Figure 15.8, to discover how its GUI makes it easy to configure name servers that provide examples in other menus of alternative possibilities.

Rather than familiarizing yourself with the proper syntax, you need only choose from the available options. Although only a limited number of options are presented, the source code is freely available if you need to modify the options. You can also request modifications from the developers.

## Testing the Connection

Entering the proper data for network settings is fine, but unless you can verify that they are correct you will still be without network connectivity. This section demonstrates a few tools that you may use to ensure that you have the software properly set up. You can also use this section as a troubleshooting guide since these are the same tools that you would use to check for problems with your connectivity. (Note, however, that this section presumes that if you are checking your system for errors, you have already made sure that the hardware is installed properly, that all cables are plugged in correctly, that the network card is seated in the motherboard, that the link lights on the card are lit, and that the interrupts are configured correctly.)

### Using the ifconfig Command

After making all the proper entries, you can start testing the viability of your network settings. The best way to verify that your network devices are working is by using the ifconfig command. Only root can change the settings displayed by this program. Any non-root user can execute the command to see what IP addresses are in use by the system. Depending upon your release, you may have to use the absolute path to the command or make sure that its location is in your path. Otherwise, you may simply want to type in the full path. On my Red Hat Linux box, the full path is /sbin/ifconfig. Listing 15.1 shows sample output for a properly configured system.

**Listing 15.1 The Output Generated by the ifconfig Command**

```
# /sbin/ifconfig -a
eth0      Link encap:Ethernet  HWaddr 00:00:C0:83:BC:7C
          inet addr:192.168.0.10  Bcast:192.168.0.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:14976 errors:0 dropped:0 overruns:0 frame:0
          TX packets:5822 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:100
          Interrupt:10 Base address:0x310 Memory:cc00-d0000

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:55636 errors:0 dropped:0 overruns:0 frame:0
          TX packets:55636 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
```

The data reported by this command show only the IP address of the current machine and whether its network device—or in this case, eth0—is up and running. It also displays the MAC address of the network device, its interrupt number, and its base memory address. The ifconfig command is useful for debugging purposes in that it shows the number of errors generated by the network delivery, including the number of collisions. The command also indicates which packets were dropped. If the card were configured incorrectly, the ifconfig command may list a large number of errors, but more than likely would not show the card at all.

Much like the ifup or ifdown commands in the /etc/sysconfig/network-scripts/ directory, the ifconfig command can also be used to bring a particular network device up or down or to enable or disable its functions. In fact, the ifup and ifdown commands are nothing more than a set of Perl scripts that utilize ifconfig along with other variables.

You can use ifconfig to accomplish the same tasks by typing ifconfig, the interface name, and the down or up variable. The following examples show how to bring down and then back up on the primary Ethernet interface:

```
# ifconfig eth0 down
# ifconfig eth0 up
```

## Configuring Additional Network Devices

The ifconfig command is also useful if you are on a system that hosts multiple virtual domains or domains that are not identified by a box but are virtual and exist within another machine. For example, the server antares.agronomy.org could also host virtual domains named stars.com and astronomy.net. Any box can host a unique domain that exists only on that machine. Each domain would then have its own unique IP address if you wanted to make certain that it is uniquely identified, provided that the name server responsible for the domain also pointed to this IP address.

You use the ifconfig command to enable the broadcast of each IP address. For example, in the /etc/sysconfig/network-scripts/ directory, you could copy the ifcfg-eth0 file to another file called ifcfg-eth0:0. This new file would then hold the information regarding this new domain name, including the IP address and hostname. Make sure that the new IP address is not the same IP address that your server currently uses, but that it still is valid and falls under a range of IP addresses that you own.

The following command, for example, defines the device eth0:0 to a specific IP address.

```
# ifconfig eth0:0      206.71.77.51
```

After entering the necessary information into that file, you can begin testing to make sure it works. Enter route -v to check the current IP addresses. Now enter the following commands:

```
# /sbin/ifconfig eth0:0 up
# /sbin/ifconfig -a
```

The last command prints out the available IP addresses in use by the system. Make sure that the command includes the newly created domain IP. Run a ping test to verify that the IP address or domain assigned to it is alive and that you are currently using the correct IP. Try pinging the box both from the local machine hosting the IP and from another networked machine:

```
# ping 206.71.77.51
```

If the test returns a response, your configuration is correct and complete. You can now begin assigning other virtual domains to the same machine.
