
## 5.5.1 Selecting Quick Setup

In this section, we will perform a quick setup to configure Tru64 UNIX in preparation for the installation of TruCluster Server. Our configuration is relatively simple because our environment is rather uncomplicated. Your environment may be more complex. We encourage you to take the time and configure Tru64 UNIX to meet your needs first before you continue with the installation and configuration of TruCluster Server. Remember that you need a solid and strong foundation before you can build on it.

In our example (see Figure 5-1), we select a “1” for “Quick Setup.” The “Quick Setup” program starts up various SysMan application menus and asks the system administrator in configuring basic services. The basic services allow the server to be on the network, do printing, and potentially send and receive e-mail.

### NOTE:

SysMan is a common interface used to configure and manage Tru64 UNIX systems and is available in GUI, menu, and command line formats.

If your system is graphics capable, then instead of seeing the setup(8) program, the checklist clipboard will appear as shown in Figure 5-2.

![](img/a0df85c2e542a8d6c913113908553aa4_133_0.png)

**Figure 5-1: The Tru64 UNIX setup Program**

### 5.5.1.4 Setup Network Routing

On this SysMan screen, we are given the ability to setup network routing. In order to do this, we need to know how routing is performed on our network.

In Figure 5-7, we use gated for network routing. While it is not essential to use gated during the configuration of a standalone, non-clustered Tru64 UNIX system, gated is a requirement for Cluster Alias to operate properly within TruCluster Server.

For your Tru64 UNIX server, you will need to determine how routing is done on your network before you can make an appropriate selection. We strongly recommend that you check with your networking group to determine this information or check the configuration of another server on your network and use that information as a prototype for your own server. For more information on networking administration, refer to Chapter 20.

### 5.5.1.5 Specify the Domain Name Service (DNS/BIND) Server

This next “Quick Setup” screen (Figure 5-8) allows us to specify the DNS Server(s) information.

Here we enter the DNS network domain and the DNS server name(s) and IP address(es).

### 5.5.1.6 Specify the Network Time Protocol (NTP) Server

This “Quick Setup” screen (Figure 5-9) allows us to enter our NTP Server information.

The NTP server information is the hostname or the hostname’s alias of the NTP server.

We recommend that you configure NTP prior to configuring the TruCluster Server software. TruCluster Server requires that the member system clocks be kept synchronized. Please refer to Chapter 20 for details on configuring NTP, including tips on using the local reference clock address (127.127.0.1) if needed.

If you choose not to use NTP Services, then we recommend that you use a time protocol that adheres to the RFC 1035 and that you not use timed(8).

### 5.5.1.7 Specify the Network Information Service (NIS) Server

Figure 5-10 is the next “Quick Setup” screen. It allows you to configure NIS Services. If you use NIS in your environment, we recommend that the system be fully configured for NIS prior to the installation and configuration of TruCluster Server. Why is this our recommendation? Because if you configure NIS on the standalone server first, then when you create the cluster, it will be propagated to each cluster member. Please note that the NIS domain is not the same as a DNS Network Domain.

For more information on setting up NIS, see the Tru64 UNIX Network Administration Guide for versions 5.0A and 5.1, or the Tru64 UNIX Network Administration: Service Guide for version 5.1A and newer.

### 5.5.1.8 Specify NFS Services

Figure 5-11 allows us to specify the NFS Services that we will be using.

Here we are enabling remote directory mounting and directory exporting. For your system, please do what is in the best interests of your users.

### 5.5.1.9 Specify E-mail Server

As most UNIX servers either send e-mail, receive e-mail, or both, we need to specify an E-mail Server to use in our configuration. This configuration is primarily for forwarding SMTP mail. For more on configuring e-mail in a cluster, please review Chapter 21.

We enter the system name for our E-mail Server as shown in Figure 5-12.

### 5.5.1.10 Specify a Default Printer and Print Server

This “Quick Setup” screen (Figure 5-13) allows us to specify a default printer and print server.

### 5.5.1.11 Quick Setup Summary and Completion

That about does it for performing a simple *Tru64 UNIX* configuration. These next two “Quick Setup” screens (see Figure 5-14) allow us to verify and potentially correct any mistakes we may have made during the selections for configuration of the system.

As we are satisfied with all entries, we select “Finish” and the Quick Setup program configures the system.

![](img/a0df85c2e542a8d6c913113908553aa4_136_0.png)

**Figure 5-3: SysMan Navigational Information**
