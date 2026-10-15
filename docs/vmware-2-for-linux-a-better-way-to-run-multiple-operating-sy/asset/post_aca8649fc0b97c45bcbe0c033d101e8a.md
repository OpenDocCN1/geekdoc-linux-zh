
If you already run a Samba (SMB) server on your Linux host OS, you should not install the VMware custom Samba server, or you might disrupt the operation of one or both of them. Many default Linux configurations incorporate a Samba server. It is possible, but experimental, to make the two work together. If you are in doubt, don't install the custom Samba server.

2. If you turn on host-only networking by answering yes in Step 1, you'll want to answer yes to the next question: Do you want this script to probe for an unused subnet? VMware looks for a family of IP addresses that it can safely use in virtual machines without causing conflicts within your LAN. If you answer yes, VMware launches a special DHCP server to provide IP addresses to your virtual machines.

Make a note of the subnet VMware decides to use. You'll need it later to configure networking between the host and virtual machine over host-only networking. The exact numbering scheme of the subnet is different from computer to computer; on my system, VMware assigns 192.168.71 as the first three digits for host-only networking. In general, the host machine is assigned as machine #1, so in this case, my host is 192.168.71.1. Virtual machines start at 128, so the first virtual machine on my computer is at 192.168.71.128.

3. If you elect not to enable host-only networking, you probably want to enable bridged networking. Bridged networking lets VMware share your Ethernet card directly, so a virtual machine appears on your LAN (and to the outside world) as a regular networked PC. This decision is pictured in Figure 4.4.

![](img/b2b6702758c230ce537468351fc8af15_68_0.png)

Figure 4.4  VMware can configure both host-only (PC-to-virtual machine) and bridged (virtual machine-to-LAN/Internet) networking.

> Host-only networking: A custom Samba implementation that allows a virtual machine to speak with your Linux host OS, even without any form of network card.

You can actually use other network protocols than Samba over the host-only networking: In fact, I advise you to do so later in the book. In general, only use host-only if you don’t have a real Ethernet card or if you have a compelling reason not to want to expose your virtual machines to an outside LAN and the Internet.

4. If you have enabled host-only networking, answer yes to the next question and designate a username and password for Samba file sharing. If you choose to skip this step, or you need to add more Samba users in the future, enter the command /usr/bin/vmware-smbpasswd vmnet1 -a <username> where <username> is the Linux user you want to configure for VMware file sharing.

If you do not configure networking support in VMware at all, I’ve got bad news: If you change your mind later, you have to uninstall and reinstall the program! When in doubt, at least configure host or bridged networking.

5. VMware’s installation is complete. It’s time to install your license key so VMware can actually start.

## Obtaining and Installing a License Key

VMware will not run without a special text file called a license key. VMware provides free license keys that are valid for 30 days on its Web site. You can also use the VMware site to purchase permanent license keys if you decide to keep using the software.

## Requesting a License Key

To obtain your 30-day trial key, follow these steps:

- 1. Open a Web browser and connect to http://www.vmware.com/forms/Download.cfm.
- 2. Fill out the form shown in Figure 4.5. You need to provide basic user registration information. Be sure you select VMware 2.0 for Linux in the Product line.
- 3. Click Register me and send my Key. After a few minutes, depending on how busy VMware’s Web servers are at the time, you should see email from VMware customer service appear in the mailbox you provided in Step 2.

TIP

CAUTION

BUZZWORD
Bridged networking: VMware shares your Ethernet card, allowing your virtual machine to have a unique hardware and IP address. In essence, bridged networking transparently splits your primary Ethernet card into two (or more).
