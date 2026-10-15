You can actually use other network protocols than Samba over the host-only networking: In fact, I advise you to do so later in the book. In general, only use host-only if you don’t have a real Ethernet card or if you have a compelling reason not to want to expose your virtual machines to an outside LAN and the Internet.

4. If you have enabled host-only networking, answer yes to the next question and designate a username and password for Samba file sharing. If you choose to skip this step, or you need to add more Samba users in the future, enter the command /usr/bin/vmware-smbpasswd vmnet1 -a <username> where <username> is the Linux user you want to configure for VMware file sharing.

If you do not configure networking support in VMware at all, I’ve got bad news: If you change your mind later, you have to uninstall and reinstall the program! When in doubt, at least configure host or bridged networking.

5. VMware’s installation is complete. It’s time to install your license key so VMware can actually start.

# Obtaining and Installing a License Key

VMware will not run without a special text file called a license key. VMware provides free license keys that are valid for 30 days on its Web site. You can also use the VMware site to purchase permanent license keys if you decide to keep using the software.

# Requesting a License Key

To obtain your 30-day trial key, follow these steps:

+   1. Open a Web browser and connect to http://www.vmware.com/forms/Download.cfm.
+   2. Fill out the form shown in Figure 4.5. You need to provide basic user registration information. Be sure you select VMware 2.0 for Linux in the Product line.
+   3. Click Register me and send my Key. After a few minutes, depending on how busy VMware’s Web servers are at the time, you should see email from VMware customer service appear in the mailbox you provided in Step 2.

TIP

CAUTION

BUZZWORD
Bridged networking: VMware shares your Ethernet card, allowing your virtual machine to have a unique hardware and IP address. In essence, bridged networking transparently splits your primary Ethernet card into two (or more).