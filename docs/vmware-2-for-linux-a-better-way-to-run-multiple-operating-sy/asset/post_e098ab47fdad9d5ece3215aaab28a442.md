
## Appendix B: File Sharing with Samba and NFS in VMware

was made for you. It’s actually blissfully easy, as long as a few crucial details match up between your host and guest.

After setting up your host Samba server as described earlier, boot up your Windows guest operating system. Any version from Windows 3.11 for Workgroups to the present supports Samba networking. This example uses Windows 98 for illustration, but the method is virtually identical in all Windows variants.

You might need to add Microsoft Networking capabilities if they were not loaded when you installed your system. The easiest way to do this is to load the Network control panel and add the Microsoft Network client. (This will likely require reading from your original Windows installation CD.)

> Unless you have a major security concern, your Microsoft Networking login (the prompt you see whenever Windows starts up) should be one of the username/password combinations you previously assigned using vmware-smbpasswd. However, don’t use your root account. It’s counter-intuitive to log in as root on Windows and it creates a number of headaches.

When Microsoft Network is installed, you are almost ready. In the Network control panel, click the Identification tab and check the settings, as shown in Figure B.1.

Although you can feel free to edit your computer name, you really only need to care about the Workgroup field, which needs to exactly match the Workgroup ID established in the /etc/vmware/vmnet1/smb/smb.conf file on the host.

![](img/b2b6702758c230ce537468351fc8af15_407_0.png)

**Figure B.1** Use the Network Identification tab in Windows to set the Workgroup to the same value used by the VMware Samba server, WORKGROUP by default.

> If you change the computer or workgroup name, you will likely need to reboot the Windows guest.

Next, click the Network Neighborhood icon. (This might be called My Network Places, depending on your version of Windows.)

As long as the Samba server is running, Microsoft Network is properly installed on the guest, and the Workgroup names match, your host computer should appear similar to Figure B.2.

Double-clicking on the host icon (in the case of my system, Jhost) should present you with a new window with two folders. HostFS refers to whatever you chose to share under the [HostFS] section of the /etc/vmware/vmnet1/smb.conf file, and you should also see a folder for the home directory of your Samba login name, as shown in Figure B.3.

![](img/b2b6702758c230ce537468351fc8af15_408_0.png)

Figure B.2 Network Neighborhood should see your Linux host as a fellow computer on the network.

![](img/b2b6702758c230ce537468351fc8af15_408_1.png)

Figure B.3 Windows sees a special HostFS directory which you can point anywhere in your Linux filesystem, as well as the home directory of the username you gave when you logged in to Windows.

Congratulations! You have successfully mounted your Linux file system in Windows. You can open Linux files in Windows directly, without an intermediate copying step, or save data to the Linux drive. You can use Windows file management tools such as Windows Explorer to browse the contents as well, as shown in Figure B.4.

![](img/b2b6702758c230ce537468351fc8af15_409_0.png)

Figure B.4 Once Samba networking is running smoothly, you can browse your Linux drives with Windows Explorer or a number of other Windows applications.

## Using Samba with a Linux Guest

You’ve read about VMware’s host-only networking and how you can use Samba to share files and directories between your Linux host and a Linux virtual machine. In truth, Samba is not necessarily the ideal way to share files between your guest and host. The standard Linux Samba client is more or less a glorified FTP interface. You can use Samba to mount drives directly, but it may be a more trouble than it’s worth, depending on your threshold for command-line tinkering and your need to link your host and guest filesystem together in a Linux virtual machine.

Although a number of clever people have worked very hard to implement Microsoft’s SMB networking standard on Linux, the fact of the matter is that configuring Samba in Linux is just plain difficult. Some people are experts in Samba configuration, and I salute them. But there’s a reason there are technical books entirely dedicated to this subject.

VMware makes a valiant attempt to automate the process of sharing drives over Samba, and if you are interested in the SMB protocol or have your own reasons for disturbing or disliking FTP, you may want to use Samba for Linux-to-Linux (or FreeBSD) networking. If you installed the default Samba server when you installed VMware, and you are not running any other Samba server, chances are good that Samba will work on the first try.
