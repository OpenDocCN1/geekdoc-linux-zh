
## Configuring Your Root Password

The first item that needs configuration is the root password (see Figure 1-21). We will talk about the root user in Chapter 2, but now it is enough to know this the user who has the privileges to change anything on the system, has access to all files on the system, and is known as a superuser.

The password should be something that you can remember, but also difficult to guess. A combination of letters and numbers is always a good way of making a strong password. Using your name, family member names, and so on should be avoided as these can be easy targets for passwords. Click Next after you've entered your root password and re-enter for verification.

## Configuring Your Network Access

If any network interface cards have been detected in the system, you will be asked to configure them for network access (see Figure 1-22). By default, YaST sets the Ethernet card it finds as your system's primary Ethernet interface and assigns it an address that is configured via the Dynamic Host Configuration Protocol (DHCP).

You can find discussions about DHCP servers in Chapter 20.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_74_0.png)

Figure 1-21: Setting the root password

# Chapter 1 | Installing SUSE 31

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_75_0.png)

Figure 1-22: Configuring network cards

For most people using SUSE in a business environment, a DHCP server may already be running, and address domain name system (DNS) server list, and router configuration will be available. Home users and users setting up a server will find it necessary to configure these details manually. Home users with simple broadband or dial-up connections often automatically receive this information from their Internet service providers (ISPs) and may not need to change these settings.

To change the configuration of the network card, "Network Interfaces" and select the network card in question (if you have multiple network cards), and click the Edit button. A similar to the one shown in Figure 1-23 appears.

In this example, we set the IP address of the network card to 192.168.0.1/255.255.255.0, with a router/gateway of 192.168.0.8 and a DNS server of 192.168.0.254. If you are unfamiliar with these terms at this stage, see Chapter 6 for additional information.

To change the configuration of the network card from automatic to manual, select Static address setup. This enables you to edit the IP and subnet mask fields. As you can see in Figure 1-23, we have set the IP address/netmask to that of the configuration we talked about in the preceding paragraph.

# Part I | SUSE Linux Basics

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_76_0.png)

Figure 1-23: Configuration of network cards

## Setting Up Your Host Name and DNS Addresses

To set up the host name of the Linux machine and the addresses of your Domain Name System servers, select the host name and name server button. A screen like that shown in Figure 1-24 appears.

The host name of your Linux machine can be anything you like, like a person's name, a descriptive name, or something random. The only thing that you have to bear in mind is that the host name and domain name can contain only letters and numbers as well as a hyphen or an underscore. The host name can be only one string of characters and cannot contain a space or a period. As the name suggests, the domain dictates the network domain that this machine falls into. This domain may be well-something in line with your company's policy or something you set up yourself.

> When integrating a new system into an existing network environment, you should always follow the same naming conventions that are already being used, especially for the domain name. If you do not, other systems on the network may not be able to locate your system correctly, and certain services on your system may not be able to interoperate with existing network services.

# Chapter 1 | Installing SUSE 33

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_77_0.png)

Figure 1-24: Configuring DNS and host name

Enter the server address into the Name Server 1 field. You can also enter up to two separate DNS server entries. Your administrator or ISP should be able to give you this information.

The Domain Search entry is used to control how your machine looks up the address of other machines connected through TCP/IP. For example, if you use a Domain Search entry as suse.com, you can communicate with any machine in the SUSE by just its host name. For example, suse.com as the Domain Search entry, you can communicate with the machine you are setting up in this example by just using the host name of bible. If you have suse.com as a Domain Search, however, you have specify the fully qualified domain name of the machine you want to communicate with (in the case of this example, that is bible.suse.com).

When you set the DNS configuration for your system, press OK to save your changes.

## Configuring the Default Gateway

Next, you will probably need to configure the gateway for your system. To do this, click the Routing button. You will see a screen similar to the one in Figure 1-25.

# Part I | SUSE Linux Basics

The default gateway is the IP address of the host to which TCP/IP packets are destined. For example, your gateway will be that of your subscriber line (ADSL) if that is how you connect. In other cases, your system administrator will be able to provide you with this information.

Enable Forwarding if the system is a router: The idea of the default route is to enable it.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_78_0.png)

Figure 1-25: Default gateway

When you have set the gateway address, click OK. You will then be returned to the Network Setup screen. If you are happy with the network configuration, click Next.

## Testing Your Connection and Online Updates

Taking a page from other operating systems, SUSE now allows you to run the update as soon as the system has been installed (see Figure 1-26). Online updates are discussed in more detail in Chapter 9 and are not discussed as part of installation. If you are feeling adventurous, testing your connection and running the online update is a good idea, but it is not necessary as part of installation. Click Next after you have made your choice.

# Chapter 1 | Installing SUSE 35

- Preparation
- Language
- License Agreement
- System Analysis
- Time Zone
- Desktop Selection
- Installation
- Installation Summary
- Partition Installation
- Configuration
- Root Password
- Network
- Online Update
- Users
- Clean Up
- Release Notes
- Hardware Configuration

## Test Internet Connection

To validate your Internet access, activate the test procedure. The following steps will be performed:

- Download latest release notes
- Check for latest updates

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_79_0.png)

Figure 1-26: Online update

## Configuring Your Modem

Modems are notorious for being something of a problem area for Linux because many of the internal PCI modems that are on sale are not true modems, but what is known as winmodems or soft modems. The idea behind winmodems is that some of the functionality of the modem can be offloaded from hardware into software — the software in question being the Windows operating system. As these devices are designed to work only with Windows and there they require a Microsoft operating system to work, it is not surprising that there are difficulties getting them to work on Linux. There are three possibilities:

- You have an old-fashioned external serial modem. These will always work under Linux.
- You have a winmodem. This may or may not work with Linux.
- You have an internal true hardware modem. In almost all cases this will work with Linux.

Winmod support has improved considerably, and some previously unsupported modems now work with Linux. SUSE supports at least the SmartLink and Lucent Itmod types. During the installation, if YaST detects that you have a supported winmodem, it will install the necessary package to provide driver support.
