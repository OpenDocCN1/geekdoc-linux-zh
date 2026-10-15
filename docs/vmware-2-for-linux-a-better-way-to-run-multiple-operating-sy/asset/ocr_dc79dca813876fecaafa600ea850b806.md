7. Enter a size for the new virtual disk. Although 2,000 is the default, you can go as high as 2,047MB, as shown in Figure 12.2. Remember that the disk grows as data is added, but you cannot change its maximum size later. Click Next to proceed.

8. VMware should detect your CD-ROM. Leave the default settings as is (to enable CD-ROM access and make it available when the virtual machine boots), and click Next.

9. VMware asks about floppy access. Unless you have a compelling reason to disable the floppy, leave this setting alone as well. Click Next.

10. The wizard asks how the virtual machine should be able to access the network (see Figure 12.3). If you plan to keep the Windows VM completely isolated, you can click No networking. If you have an Ethernet card installed and your PC is on a LAN, use Bridged networking, which lets the virtual machine share your Ethernet card and appear as a standalone computer on the network. Host-only networking allows Samba file sharing between the VM and your Linux PC (provided you installed the VMware Samba server at installation or have one of your own running), and Bridged and Host-only networking combines the two. If you have a LAN, stick with Bridged for now. If you do not, use Host-only or none. Click Next to reach the final step.

See Chapter 9, "Using Your Windows 95/98 Virtual Machine," and Appendix B, "File Sharing with Samba and NFS in VMware," for extended file sharing and networking tips for Windows.

11. The wizard summarizes the virtual machine it will create. Figure 12.4 shows a sample configuration. If everything looks appropriate, click Done.

![](bbox=[0.25, 0.8, 0.62, 0.95])

Figure 12.2 Try to maximize your virtual disk space, because Windows 2000 is hungry for storage.