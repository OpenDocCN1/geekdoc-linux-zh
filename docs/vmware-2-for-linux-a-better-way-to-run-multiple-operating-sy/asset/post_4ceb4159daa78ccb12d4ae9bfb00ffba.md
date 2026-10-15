
**Table 3.1 Quick Reference of VMware System Recommendations**

| Resource | Recommended |
|---|---|
| Linux host OS | Red Hat 5.x and above, SuSE Linux 6.0 and above, OpenLinux 2.2 and above, TurboLinux 6.0 and above |
| System CPU | 266MHz CPU minimum (500+ MHz recommended) |
| System RAM | 96MB + 32-128MB per simultaneous virtual machine |
| Disk space | 2GB per virtual machine minimum |

## Chapter 4: Installing VMware for Linux

- Installing from the included CD
- Deciding how you want to network
- Obtaining and installing a license key
- Troubleshooting the install
- Checking for updates online

All right, enough studying. You now know plenty about VMware theory—certainly enough to take the plunge and actually install it on your PC. So get out the book’s included CD (if you haven’t already) and let’s get started!

### Installing from the Included CD

This book comes bundled with a CD-ROM that contains, among other things, the core VMware binaries. It should take only a few minutes to install VMware from the CD-ROM, and after visiting the VMware Web site to request a free 30-day trial license, you can start running guest operating systems on your Linux PC.

Earlier versions of VMware sometimes required users to download a special version of the XFree86 server, and you might find some reference to this requirement in VMware documentation. But recent versions of XFree86 (which you should have installed, if your system meets the requirements outlined in Chapter 3, “Equipping Your PC for VMware”) eliminate this problem, and you shouldn’t need to worry about it.

1. If you haven’t already, log in to Linux and start X Windows with the user account you will use for running VMware.
2. Open a terminal window.
3. Insert the VMware CD-ROM, and mount it as you normally would if your system does not automatically mount newly inserted CDs (usually by typing mount /dev/cdrom).
4. The CD contains a directory called VMware Binaries, which contains the VMware installation program. cd to this directory off the mountpoint used by your CD-ROM drive. (Often it is cd "/mnt/cdrom/VMware Binaries". Quotes are necessary because the directory contains a space.)
5. Copy the file VMware-2.0.1-570.i386.rpm to a working directory on your hard drive.

> If your system does not support RPM package installs, copy the file VMware-2.0.1-570.tar.gz instead, and watch for modified instructions ahead.

6. If you do not normally run as root (yes, all the books tell you not to, but some people still do it!), you need the root password and the ability to use the su (superuser) command.

![](img/b2b6702758c230ce537468351fc8af15_65_0.png)

7. Use cd to change to the working directory that holds the .rpm or .tar.gz file. If you are using the .tar.gz file, skip to Step 9.
8. Start the installation process with the command rpm -Uhv VMware-2.0.1-570.i386.rpm. Your screen should resemble Figure 4.1. Skip to Step 12.

![](img/b2b6702758c230ce537468351fc8af15_66_0.png)

Figure 4.1 RPM unpacks VMware and prepares your system for installation.

> If you already have an earlier version of VMware installed on your PC, the preceding command should still work because the "U" in rpm -Uhv tells the package installer to update any existing instances of VMware.

> If you’re comfortable with other RPM package installers, such as GnoRPM, you should be able to use them without any problems.

9. The .tar.gz file needs to be uncompressed. Type tar -xzf VMware-2.0.1-570.tar.gz.
10. Uncompressing the archive creates a new directory, vmware-distrib. Use the cd command to change to vmware-distrib.
11. Type ./vmware-install.pl. This installs important VMware files to vital locations on your hard drive. Accept the default values prompted. If you are offered the chance to run vmware-config.pl, accept it and proceed to the next section, "Deciding How You Want to Network." If you do not want to start the configuration of VMware at this time, read Step 12 when you are ready.
12. At the current terminal prompt, type vmware-config.pl. The installation officially begins, as shown in Figure 4.2.
13. Press Enter to read the VMware EULA. Page through with the Space key, type yes, and press Enter to accept. VMware then analyzes your system for compatibility, and if all is well, it proceeds to the next step.
