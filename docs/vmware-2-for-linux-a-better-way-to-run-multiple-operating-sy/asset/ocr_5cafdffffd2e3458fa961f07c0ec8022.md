Most modern Linux installation CD-ROMs are self-booting, and virtual machines can boot from CD-ROM, so you might not need to use a Linux boot floppy. Still, if you have a floppy drive available, it’s safest to let VMware use it.

10. The wizard asks how the virtual machine should be able to access the network, as shown in Figure 10.4. If you plan to keep the Linux VM completely isolated, you can click No networking. If you have an Ethernet card installed and your PC is on a LAN, use Bridged networking, which lets the virtual machine share your Ethernet card and appear as a standalone computer on the network. Host-only networking allows file sharing and communication between the VM and your Linux PC but not with the outside world. If you plan to use Host-only networking, it is best if you let VMware install its own Samba and DHCP server (as advised in Chapter 4, “Installing VMware for Linux”). Bridged and Host-only networking combines the two. If you have a LAN, stick with Bridged for now. If you do not, use Host-only or none. Click Next to reach the final step.

Even if you don’t install any networking, there is still an easy way to exchange files between your Linux PC and virtual disks. It involves mounting the virtual disk as a Linux-readable file system, which is covered in depth later in this chapter. It avoids a great deal of hassle.

![](bbox=[0.12, 0.71, 0.55, 0.92])

Figure 10.4 Choose a networking option so that the Linux virtual machine can communicate with the host OS, and/or the outside world.