
After all of the packages install, the installer displays a message informing you that installation is complete. Eject the DVD and click the Exit button to reboot your PC. You can then perform additional configurations and install additional software.

## Configuring the firewall and SELinux after first boot

When you first reboot your PC after completing the Fedora Core installation, a first-time configuration utility takes you through a number of additional configuration steps that include accepting a license agreement, configuring the firewall and SELinux, selecting the colors and resolution for the display, setting up a user account, and checking the sound card. Of these steps, the configuration of firewall and SELinux is important for your system’s security, so I briefly describe these steps next.

In the firewall and SELinux configuration steps, you configure the built-in packet filter that comes with Linux, select the level of Security Enhanced Linux (SELinux) access control, and customize these security levels to suit your needs.

Note that SELinux is a mandatory access control framework developed by the National Security Agency (NSA), a U.S. government agency, and is included in Linux kernel 2.6. You can find more about SELinux at the NSA Web site, www.nsa.gov/selinux. To explain briefly, SELinux access control goes beyond the traditional access control in Linux, which is based on the user and group ID that owns a process or a file. SELinux views the system in terms of *subjects* (users or processes) and *objects* (files, devices, any system resources). Subjects can take on different roles, such as *normal user* or *system administrator*. Each subject also has a domain, and each object has a type. SELinux provides fine-grained control over who can access what in a Linux system by defining what domains can access what types and how one domain can transition into another when programs execute. It sounds confusing, but you don’t need to understand everything to enjoy the increased security provided by SELinux.

For the firewall, you have to select one of the following options:

- **Disabled** means that the firewall is not active and your system accepts all types of connections without performing any security checking. Use this option only if your system runs on a trusted network or if you plan to set up a firewall configuration later on (the sooner the better).
- **Enabled** means that you want to set up a firewall. This means that your system does not accept any connections other than those that you explicitly enable. By default, the system accepts only DNS and DHCP requests. You can then select the services, such as Mail and FTP, which are allowed to pass through the firewall.

For the SELinux access control configuration, you can set it to one of the following options:

- **Enforcing** means SELinux enforces mandatory access control.
- **Permissive** means SELinux prints warning messages but does not actually enforce the access control policies.
- **Disabled** means SELinux is turned off.

You can also modify SELinux policy from the configuration screen, but it’s safe to leave the SELinux access control set at its default setting.

When you’ve gone through all the configuration steps after the first reboot, click Finish to get Fedora Core’s graphical login screen and start using Fedora.

## Installing ME Pis

The companion DVD includes a single-CD ISO image for the MEpIS distribution — called SimplyMEPIS — that you can burn onto a CD and use as a Live CD as well as an installation CD. (MEPIS, by the way, is pronounced MEE-pis.) When you boot from the MEpIS CD, MEpIS runs directly off the CD, and you get the MEpIS Live CD login screen, where you can log in using one of two predefined usernames: demo or root.

- **Run the Live CD**: To try out MEpIS as a Live CD system, click Demo in the login window and type demo as the password.
- **Install the distribution**: To install MEpIS, click the Root icon in the login window and type root as the password.

When you log in as root, you get the MEpIS desktop with a red background, as shown in Figure 2-10 (trust me, it’s red: The red background reminds you that you are logged in as root). From this desktop you can start the MEpIS hard drive installation.

To install MEpIS on your PC’s hard drive, follow these steps:

1. Click the INSTALL ME icon on the MEpIS desktop (see Figure 2-10).

The MEpIS OS Center window opens (see Figure 2-11). From the MEpIS OS Center you can perform a number of system configuration maintenance tasks, including installation of MEpIS onto a hard drive.

![](img/11709a8f88c8cd03868a929dc94c0e2b_83_0.png)

2. Select **Install MEPIS on Hard Drive** from the list of tasks shown on the left side of the MEPIS OS Center window.

The MEPIS OS Center displays the copyright notice on the right side of the window, as shown in Figure 2-11.

![](img/11709a8f88c8cd03868a929dc94c0e2b_83_1.png)

3. Read the copyright notice, and if you agree, click Next to continue.

The MEPIS OS Center displays the first step of installation, which includes three parts:

- Select the hard drive for installation.
- Run QTParted to rearrange partitions. This step is optional, but if you have an existing Windows partition and need to create space for MEPIS, click the Run QTParted button to shrink the Windows partition using QTParted. (For more information, see the “Resizing a partition with QTParted in Knoppix” section in this chapter.)
- Select whether you want to install using the whole disk or using a set of existing hard drive partitions. I installed after I had created some partitions, so I selected the option to install on existing partitions. If you elect to install on existing partitions, MEPIS OS Center gives you the option to select partitions for the file system root, the /home directory, and the swap partition. You have to designate one partition for the root and another for swap.

4. Assign the root partition — the partition to be used for the file system’s root — and the swap partition and click Next.

The MEPIS OS Center displays a dialog box asking for confirmation that you really want to format and destroy all data in the assigned partitions. Click Yes to get the MEPIS installation started. After copying the files from the CD to the hard drive, the MEPIS OS Center proceeds to installing the GRUB boot loader and selecting the kernels you want to boot.

5. Select whether you want to install GRUB on the master boot record (MBR) and the kernel versions — 2.4 and 2.6 — that you want to install.

You can usually accept the default choices of installing GRUB on the MBR and booting the 2.6 version of the kernel.

6. After making your selections, click Next to continue.

7. Enter the root password and define a normal user account. Then click Next.

8. Enter the host name and domain for the computer as well as the Windows workgroup name. Then press Enter.

9. Select what services to start, including the Guarddog firewall service. Also select the display driver. Then click Next.

10. Set the keyboard layout and the clock. Then click Next.

11. Click Finish to complete the MEPIS installation.

The message on the final installation step informs you that you can get community support for MEPIS at www.mepis.org or www.mepislovers.com.

After you remove the CD and reboot, you get the GRUB menu from which you can boot MEPIS from your hard drive. You can then log in as a normal user with the username you defined when you installed MEPIS.

## Installing SUSE Linux

The companion DVD does not include the full SUSE (I pronounce SUSE SOO-za, but many people say it differently) Linux distribution from the openSUSE project because of limited space on the DVD. Instead, the DVD includes the ISO image file for a SUSE Live DVD that enables you to run SUSE Linux directly from the DVD. You can download the full SUSE Linux distribution from http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/.

![](img/11709a8f88c8cd03868a929dc94c0e2b_85_0.png)

To try the SUSE Linux Live DVD version, simply burn a DVD from the SUSE Live DVD ISO image on this book’s companion DVD and then boot your PC from that DVD (you need a DVD burner to burn the ISO file on DVD media).

To install the full SUSE distribution, you have two options:

- Install the full distribution directly over a high-speed Internet connection from one of the FTP servers that mirror the SUSE Linux distribution.
- Install the full distribution by downloading and burning 5 CDs from the SUSE Linux ISO images at http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/, and then booting your PC from the first CD. (For instructions on burning the CD, turn to the “Burning CDs or DVDs from ISO Images” section in this chapter.)

In the following sections, first I go over the steps for performing an FTP install, and then I describe the full SUSE install from the CDs.

## Performing an FTP install

To install SUSE Linux from one of many FTP servers that mirror the SUSE distribution, you have to perform the following major steps:

1. Download the SUSE boot image from the FTP server and burn a CD with that image.
2. Make a note of the FTP server’s IP address and the directory where the SUSE distribution’s files are located.
3. Boot the PC with the boot CD. Type a command at the boot prompt to begin an FTP install from the FTP server that you identify by its IP address.
