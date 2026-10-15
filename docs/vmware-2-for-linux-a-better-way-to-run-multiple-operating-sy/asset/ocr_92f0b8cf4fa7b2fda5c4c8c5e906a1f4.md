# Appendix B: File Sharing with Samba and NFS in VMware

was made for you. It’s actually blissfully easy, as long as a few crucial details match up between your host and guest.

After setting up your host Samba server as described earlier, boot up your Windows guest operating system. Any version from Windows 3.11 for Workgroups to the present supports Samba networking. This example uses Windows 98 for illustration, but the method is virtually identical in all Windows variants.

You might need to add Microsoft Networking capabilities if they were not loaded when you installed your system. The easiest way to do this is to load the Network control panel and add the Microsoft Network client. (This will likely require reading from your original Windows installation CD.)

> Unless you have a major security concern, your Microsoft Networking login (the prompt you see whenever Windows starts up) should be one of the username/password combinations you previously assigned using vmware-smbpasswd. However, don’t use your root account. It’s counter-intuitive to log in as root on Windows and it creates a number of headaches.

When Microsoft Network is installed, you are almost ready. In the Network control panel, click the Identification tab and check the settings, as shown in Figure B.1.

Although you can feel free to edit your computer name, you really only need to care about the Workgroup field, which needs to exactly match the Workgroup ID established in the /etc/vmware/vmnet1/smb/smb.conf file on the host.

![](bbox=[0.2, 0.623, 0.45, 0.857])

**Figure B.1** Use the Network Identification tab in Windows to set the Workgroup to the same value used by the VMware Samba server, WORKGROUP by default.