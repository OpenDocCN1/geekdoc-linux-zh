

![](img/b2b6702758c230ce537468351fc8af15_275_0.png)

Figure 13.6 You do not need to adjust the FreeBSD kernel before installation.

6. The FreeBSD installer Main menu appears (see Figure 13.7). You might want to take a moment to read the Usage portion to familiarize yourself with the keystrokes used by the installer.

7. If you are using host-only networking, or bridged networking with a DHCP server on your LAN, head for the Options screen, shown in Figure 13.8. Scroll down until you reach the DHCP entry, and press the spacebar to change DHCP configuration to YES. Press Q to exit back to the main menu.

![](img/b2b6702758c230ce537468351fc8af15_275_1.png)

Figure 13.7 FreeBSD uses a text-only installation program.

![](img/b2b6702758c230ce537468351fc8af15_276_0.png)

Figure 13.9 Enable DHCP for host-only networking, or a bridged networking setup that includes a DHCP server on your outside LAN.

8. Start a Standard installation from the main menu. The install program opens a disk-partitioning program, displayed in Figure 13.9. If you are using a fresh virtual disk, simply use the A command to automatically partition the entire virtual disk, and then press Q to continue.

9. Unless you plan to install additional operating systems on this virtual disk, you can safely choose any option when asked about a boot manager. If unsure, accept the default choice of installing a true boot manager.

![](img/b2b6702758c230ce537468351fc8af15_276_1.png)

Figure 13.9 Use the automatic settings to quickly partition your virtual disk.

If you use a raw disk that has other partitions, you need to be very careful here. Don't install a boot manager unless you are sure it won't cause problems with your other partitions.

10. FreeBSD asks for further disk partitioning information, as shown in Figure 13.10. Again, unless you are using a raw disk or have special requirements, use the A command to automatically partition the drive, and then press Q to quit.

11. You have to choose how thorough of an installation you want to perform in the screen shown in Figure 13.11. A good intermediate choice is X-Kern-Developer: You get XWindows, development software, and kernel sources, which are often required to compile and install complex programs. Make the choice most appropriate to your needs by highlighting the option and pressing the spacebar.

12. You are asked about installing cryptographic software. Read the instructions and answer as best suits you. If you choose to install crypto software, you are asked to select from specific crypto packages.

13. FreeBSD can install a few thousand compatible software packages. The initial disk space hit is fairly minimal, so answer Yes when asked.

14. When the XFree86 configuration screen appears (see Figure 13.12), simply accept the defaults by selecting Exit.

![](img/b2b6702758c230ce537468351fc8af15_277_0.png)

Figure 13.10 Take advantage of the express configuration settings unless you are using a raw disk with more than one operating system.

![](img/b2b6702758c230ce537468351fc8af15_278_0.png)

Figure 13.11 Select the canned distribution that best meets your FreeBSD needs.

![](img/b2b6702758c230ce537468351fc8af15_278_1.png)

Figure 13.12

15. You have another chance to select new packages and then are asked what media you want to install the system from. Select CD-ROM.

16. FreeBSD gives you one last chance to back out of the installation. Answer Yes to commit.

17. The setup program copies programs from the CD-ROM to the virtual disk for some time. When it's finished, you are asked to configure specific devices.

![](img/b2b6702758c230ce537468351fc8af15_279_0.png)

Make a note of the FreeBSD configuration tool that you can run after the installation is complete in case you need to change options: /stand/sysinstall.

18. When asked to configure Ethernet or SLIP/PPP by the screen shown in Figure 13.13, answer Yes.

19. Configure each of the network devices (one or two virtual Ethernet cards, depending on the choice you made in the VMware Configuration Wizard, and SLIP or PPP, as appropriate). If you enabled DHCP in the early stages of the FreeBSD installation, FreeBSD tries to acquire IP information automatically. A sample IP configuration screen is shown in Figure 13.14.

20. Answer Yes when asked whether your computer is a "leaf node."

21. When asked about anonymous FTP connections, answer as you see fit. (If you are worried about security, answer Yes to deny anonymous FTP access.)

22. You are asked first whether you want to enable the NFS server, then the NFS client. If you want to enable NFS file sharing between the Linux host (or other virtual machines or other computers on your LAN) and the FreeBSD machine, enable either or both.

![](img/b2b6702758c230ce537468351fc8af15_279_1.png)

Figure 13.13 Be sure to choose at least one networking option if you plan to communicate with the outside world from the virtual machine.

