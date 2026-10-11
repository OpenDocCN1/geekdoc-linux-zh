# Network-Based Installations

Although less common than CD-ROM, DVD, or hard disk installations, you can also choose to use installation media that is stored on another machine and is accessible across a network via a network interface card (NIC) in the computer. With this method of installation, you must create an installation startup CD-ROM or bootable USB flash memory drive as described in the previous section; they contain common NIC drivers and programs that allow you to connect to a server with the appropriate installation files via one of the following protocols:

+   - Network File System (NFS)
+   - File Transfer Protocol (FTP)
+   - Hypertext Transfer Protocol (HTTP)

![](bbox=[0.15, 0.36, 0.25, 0.39])

> The configuration of NFS, FTP, and HTTP is discussed in Chapter 15, “Linux Networking.”
> 
> Linux can also be installed across the network from a Windows server hosting the installation files. This method uses the Server Message Block (SMB) protocol and must be set up manually in Red Hat Linux; as a result, it is not discussed here.

After the installation startup CD-ROM or bootable USB flash memory drive has been imaged, you can simply boot the client computer using it and choose the appropriate options in Figures 7-7, 7-8, and 7-9, shown previously.

Next, you are prompted to choose either a NFS, FTP, or HTTP installation, as shown earlier in Figure 7-10. Regardless of the installation type chosen, you are then prompted to configure the network settings, as shown in Figure 7-12. The values for the IP address and subnet mask are typically assigned by the Internet service provider (ISP) or the network administrator, so that the computer using the IP address can communicate with the correct set of machines on the network. You can, however, choose to receive the configuration from a DHCP or BOOTP server on the network automatically. The default gateway and the primary DNS name server are optional if configuring manually, but should be used if the values are known.

If you chose an NFS installation in Figure 7-10, the installation prompts for the DNS name or IP address of the NFS server on the network and the directory on the NFS server that contains the installation files, as shown in Figure 7-13.