
![](img/2045828cf45e5632bf056f9ca99d6755_103_0.png)

FIGURE 3.9 Harness the flexibility of logical volumes through Fedora’s easy-to-use utility.

![](img/2045828cf45e5632bf056f9ca99d6755_103_1.png)

FIGURE 3.10 Use this screen to define the logical volumes that make up your logical group.

You have to create at least two partitions: the `/` partition and the swap partition. However, you can add several mount points depending on your specific requirements. Some users find it helpful to create a separate `/home` partition, which we do in our example. As you add each logical volume, it appears in the main LVM Group options screen (refer to Figure 3.9). When you are finished, click the OK button to return to the main partition screen, which should look similar to Figure 3.11.

Now you are ready to proceed to the next screen by clicking the Next button.

![](img/2045828cf45e5632bf056f9ca99d6755_104_0.png)

**FIGURE 3.11** The completed masterpiece. It is worthwhile spending extra time to get the best partition layout for your requirements.

## Choosing, Configuring, and Installing the Boot Loader

After you accept the partitioning scheme, a screen appears asking you to select a boot loader for booting Fedora (see Figure 3.12). This screen also enables you to choose not to use a boot loader (when booting from removable media, a commercial boot utility, a DOS partition, or over a network), and the ability to boot other operating systems if you have configured a dual-boot system. Review “The Boot Loader,” previously in this chapter, for more information on making this choice.

> **TIP**
> Fedora works well with other operating systems, but the reverse is not always true. If you need specialized help with configuring a dual-boot system, check various HOWTOs at http://www.tldp.org for hints and tips.

Select the GRUB boot loader. GRUB is typically installed in the MBR of the first IDE hard drive in a PC. However, the boot loader can also be installed in the first sector of the Linux boot partition, or even not installed on the hard drive. Note that you can also backtrack through the install process to change any settings.

Note that you can assign a password for the boot loader. If you choose to use this option, you have to enter a password at the GRUB boot screen (see the section “Logging In and Shutting Down” at the end of this chapter for information on graphical logins). Carefully note the password! It does not have to be the same password used to log in, but if you password protect booting through your computer's BIOS and use a boot loader password here, you will subsequently need to enter three passwords (BIOS, boot loader, and login) to access Linux. Type in a password of at least eight characters twice (once on each line); then click OK or Cancel to exit the dialog.

![](img/2045828cf45e5632bf056f9ca99d6755_105_0.png)

**FIGURE 3.12** Select whether you want to use a boot loader and configure other boot options.

> **NOTE**
> If you are planning to dual boot your PC with Windows, it will appear in the list of boot options as Other. You can click the Edit button to access options that enable you to rename it something a little more informative, or even set Windows as the default option for GRUB.

If you click the Configure Advanced Boot Loader Options button, you are asked for arguments to pass to the Linux kernel before booting. Kernel arguments are used to enable or disable various features of Linux at boot time. If you install the source to the Linux kernel, you will find documentation about the more than 200 different kernel arguments in the file `kernel-parameters.txt` under the `/usr/src/linux/Documentation` directory. Click Next to set your boot loader configuration. You then proceed to network interface configuration, as shown in Figure 3.13.

![](img/2045828cf45e5632bf056f9ca99d6755_106_0.png)

**FIGURE 3.13** Select or enter networking configuration information.

## Network Configuration

If you have an installed network adapter, you are asked for network configuration details, as shown in Figure 3.13. Fedora can be set to automatically configure networking upon booting. Note that you can also configure networking following installation using Fedora’s `system-config-network` graphical network administration tool (see Chapter 14, “Managing Users,” for details about using these tools).

> **NOTE**
> If the Linux kernel finds more than one network interface installed on your computer, you might be asked to configure a second ethernet device. This might be the case, for example, if you are installing Fedora on a computer that serves as a gateway or firewall. If you configure more than one ethernet device, the device named `eth0` will be the first active interface when you start Fedora.

You can choose to have your interface information automatically set using DHCP. Otherwise, especially if you are configuring a DHCP server, manually enter an IP address, hostname, or gateway address (such as for a router), along with DNS information if you click the Edit button listed by the interface (such as `eth0` in the example). After making your selection, click Next to continue.

# Setting the Time Zone

You are next shown a Time Zone Selection dialog (see Figure 3.14). There are two “clocks,” or times, when using a PC: the hardware clock, maintained by hardware in the computer and a backup battery; and the system time, set upon booting and used by the Linux kernel. It is important to keep the two times accurate and in synchronization because automated system administration might need to take place at critical times. Many computer installations use computers with hardware clocks set to GMT, which stands for Greenwich Mean Time. The more modern designation is UTC or Coordinated Universal Time. The Linux system time is then set relative to this time and the default time zone, such as Eastern Standard Time, which is −5 hours of UTC.

![](img/2045828cf45e5632bf056f9ca99d6755_107_0.png)

Select your time zone.

Setting the computer’s hardware clock to UTC (GMT) has the advantage of allowing the Linux system time to be easily set relative to the geographic position of the computer and resident time zone (such as a Linux laptop user who would like to create files or send electronic mail with correct timestamps, and who has traveled from New York to Tokyo). See Chapter 4, “Post-Installation Configuration,” for details on setting the date and time for Linux.

> Read the man page for the hwclock command to learn how to keep a running Linux system synchronized with a PC’s hardware clock. See Chapter 4 for more details on using the hwclock command and Linux time-related software.

Choose your time configuration, and then click Next.

# Creating a Root Password and User Accounts

You are next asked to enter a root operator password, as shown in Figure 3.15. Type in a password, press Tab or Enter, and then type it again to make sure that it is verified. The password, which is case sensitive, should be at least eight characters (or more) and consist of letters and numbers. Note that the password is not echoed back to the display. Your root password is important because you need it to perform any system administration or user management with Fedora.

![](img/2045828cf45e5632bf056f9ca99d6755_108_0.png)

FIGURE 3.15 Type in, and do not forget, your root password.

> **CAUTION**
> Do not forget your system's BIOS, boot loader, or root passwords! Some equipment, such as notebook computers, might require factory replacement of motherboard components if the owner forgets the BIOS password. The BIOS settings on most desktop PCs can usually be reset via a jumper or removal and insertion of the motherboard battery. If you forget your boot loader password, use a boot disk (perhaps created during installation as shown later on in this chapter) or boot to a rescue mode using your Fedora disc and reset the root password using the passwd command.

When finished, click Next to continue with software package selection for your new server.
