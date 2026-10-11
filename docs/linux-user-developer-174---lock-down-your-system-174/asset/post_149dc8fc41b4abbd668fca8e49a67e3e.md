
## Feature
Lock down your system

### PROTECT NETWORKS WITH IPFIRE

Quickly set up a highly customisable firewall for all your networks

IPFire is an open source firewall Linux distribution. This is an oversimplification, however, as it offers a number of other features such as intrusion detection and support for Open/VPN. IPFire takes a serious approach to security through using an SPI (stateful packet inspection) firewall built on top of netfilter.

The setup process allows you to configure your network into different security segments. Each segment is colour-coded. For instance, the green segment is a safe area representing all regular clients connected to the local wired network. The red segment represents the internet.

No traffic can pass from red to any of the other segments unless specifically configured in the firewall. The default setup is for a device with two network cards with a red and green segment only. However, during the setup process you can also set up a blue segment for wireless and an orange one known as the ‘DMZ’ for any public servers.

Once setup is complete, you can configure additional options and add-ons through an intuitive web interface. IPFire is specifically designed for people without large amounts of networking experience and can be deployed in minutes.

![](img/1f330653f83dcf0397f7d224ce8bbc16_27_0.png)

> No traffic can pass from red to any of the other segments unless specifically configured in the firewall

![](img/1f330653f83dcf0397f7d224ce8bbc16_27_1.png)

### 01 Download and install IPFire ISO

Visit www.ipfire.org/download in order to download the 162MB ISO of IPFire (or get it from the cover disc). The default hardware requirements are very minimal. Click on Other Download Options to obtain flash images as well as versions compiled for ARM architectures. The IPFire site cautions that the software doesn’t run well on devices like the Raspberry Pi, nor does it make use of the hardware random number generator. Consider having a dedicated server for IPFire or running it inside a virtual machine.

![](img/1f330653f83dcf0397f7d224ce8bbc16_27_2.png)

### 02 Run IPFire setup

The initial setup process is very simple. Select your language and use the space bar to indicate you’ve accepted the terms of the GNU licence. You will then see a notification saying that the system has been installed. The device will restart, at which point you will be asked to select your time zone. Next, you will be asked to select a root password to access the IPFire command line, as well as an admin password for accessing the web interface later on.

![](img/1f330653f83dcf0397f7d224ce8bbc16_27_3.png)

### 03 Choose network configuration type

Having chosen a host name and local domain settings, you will be taken to the Network Configuration menu. As outlined previously, the default settings are ‘GREEN + RED’. These represent devices with Ethernet attached. If you wish to set up wireless (blue) or a public server (orange-DMZ), select the ‘Network Configuration’ type option, then use the arrow keys to select a different setup. You can change these options post-install but as IPFire cautions, a network restart is required, as well as reassignment of drivers (see Step 4).

![](img/1f330653f83dcf0397f7d224ce8bbc16_28_0.png)

### 04 Choose driver assignments

Next, in the Network Configuration menu, choose Drivers and Card Assignments. You will now see the Extended Network menu. Select Green in the first instance. The menu will ask you to choose the network card for this interface. If you are unsure which to choose, click Identify and the lights on the port in question will flash for ten seconds.

![](img/1f330653f83dcf0397f7d224ce8bbc16_28_1.png)

### 05 Set network addresses

Select Address Settings from within the Network Configuration menu. You will then be asked to select the interface in question. Green allows you to assign any valid IP address for a private network here, for instance 192.168.0.1. There are more options for the Red interface, which may vary depending on your ISP. If you do choose to assign a static IP, assign it to a different subnet. For example, if green is 192.168.0.X, red could be 192.168.2.X. If you are unsure, choose DHCP.

![](img/1f330653f83dcf0397f7d224ce8bbc16_28_4.png)

### 06 Configure DNS and gateway

Back in the Network Configuration menu, choose DNS and Gateway Settings. If you chose DHCP when configuring the Red interface, your ISP's DNS servers will be used by default and you do not have to configure this further. If you chose a static IP or wish to use a different DNS server such as OpenDNS, enter them here, leaving the Gateway field blank for now. A full list of public DNS servers is available from: [wiki.ipfire.org/en/dns/public-servers].

![](img/1f330653f83dcf0397f7d224ce8bbc16_28_2.png)

### 07 Configure DHCP server

Click on Done on the Network Configuration menu to configure the DHCP server for the 'green' interface. Use the space bar to enable, and then specify your desired range of addresses within the same subnet as your green interface. For instance, if the IP address of your green interface is 192.168.0.1, you could choose a range of 192.168.0.10 to 192.168.0.39. Note that the 'Primary IPFire DNS address' is the same as the IP address of your green interface. This is because IPFire uses a DNS proxy. Leave this as is for now.

![](img/1f330653f83dcf0397f7d224ce8bbc16_28_5.png)

### 08 Open web interface

Once setup is complete, IPFire will restart and load the firewall. You will see the IPFire Console. Log in as root with the password you previously chose if you wish, then run ifconfig to check that your interfaces are in order.

You can access the web interface from any device connected to the network by opening your web browser and entering https://ipfire.localdomain:444. As IPFire uses a self-signed certificate, you may need to confirm a security exception. Enter the username admin and the password you chose previously to display the web interface.

![](img/1f330653f83dcf0397f7d224ce8bbc16_28_3.png)

### 09 Configure firewall

The web interface is easy to follow. Take some time to work through it to use IPFire's Intrusion Detection System or set up a VPN. For now, click Firewall > Firewall Rules > New Rule. The layout is fairly easy to follow. For instance, if you wish to force clients to block all external DNS servers to prevent DNS hijacking, select GREEN in the Standards Network menu to indicate you wish only to use IPFire's DNS proxy. Choose RED in the same menu in the Destination section. Finally, under Protocol select DNS and make sure REJECT is highlighted. For a full rundown of the various configurations, consult IPFire's firewall documentation at: [wiki.ipfire.org/en/configuration/firewall/start].

## STAY SECURE WITH GOOGLE AUTHENTICATOR

Secure your SSH connections with minimal fuss through two-step verification

![](img/1f330653f83dcf0397f7d224ce8bbc16_29_0.png)

For system administrators, connecting to servers via SSH is part of a daily routine for running updates and modifying files, but this can leave the system open to exploitation.

While you can reduce the chance of this happening by following some SSH best practices such as disabling root log-on, changing the default SSH port and using long passwords, the previously mentioned tools (Sparta in particular) demonstrate how easily vulnerable ports can be scanned and how passwords can be brute-forced.

Even using programs like fail2ban to limit unsuccessful login attempts or to ban certain IPs for a certain amount of time is no magic bullet, as many exploitation tools can perform several parallel tasks.

The security of your SSH server can be hugely increased through Google Authenticator. This application uses two-step verification services based on a TOTP (time-based one-time password) algorithm. The authenticator works in tandem with a mobile app, providing 6-8 digit one-time passwords that are required in addition to a username and password. Note that our guide assumes you are using OpenSSH server, which is the standard for almost all versions of Linux.

### 01 Installation

For Debian-based servers, run:

```
apt-get install libpam-google-authenticator libpam0g-dev
```

...to try to install the authenticator and related software from the repositories. Red Hat, Fedora and CentOS users should run:

```
yum install pam-devel google-authenticator
```

If Google Authenticator doesn’t exist in your distribution’s repositories, you can download and compile with the make command from github.com/google/google-authenticator.

PAM (pluggable authentication module) must also be downloaded and compiled from github.com/google/google-authenticator-libpam

Consider installing the 'ntp' daemon if you have not done so already to ensure the system time is correct, as the Authenticator uses time-based codes.

![](img/1f330653f83dcf0397f7d224ce8bbc16_29_1.png)

### 02 Generate private key

To begin, run the google-authenticator command. Press ‘y’ to indicate you wish authentication tokens to be time-based.

Next, the authenticator will display information about your secret key, along with a QR code which you can scan using the mobile app. You will also see emergency 'scratch' codes, which can be used to log in if you ever cannot access your mobile device.

Write down this information in a safe place before continuing, then press ‘y’ to update your home folder.

![](img/1f330653f83dcf0397f7d224ce8bbc16_29_2.png)

### 03 Finalise Google Authenticator preferences

The authenticator will next ask if you wish to disallow multiple uses of the same authentication token. As the authenticator states, selecting this makes man-in-the-middle attacks much harder. You can increase the 30-second period for which tokens are valid in the next step (if you wish).

Finally, if you do not already have any programs such as fail2ban installed to prevent brute-force attacks, consider pressing ‘y’ to enable rate limiting. This limits attacks to no more than three login attempts every 30 seconds.
