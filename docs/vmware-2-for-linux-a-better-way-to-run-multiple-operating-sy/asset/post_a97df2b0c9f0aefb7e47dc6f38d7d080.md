
![](img/b2b6702758c230ce537468351fc8af15_198_0.png)

Figure 10.12 *You need to load Corel Linux to a command prompt the first time you boot the installed virtual machine.*

![](img/b2b6702758c230ce537468351fc8af15_198_1.png)

Figure 10.13 *Click VMware Tools Install to attach the virtual floppy disk containing VMware Tools.*

+   5. Type `mount -t vfat /dev/fd0 /mnt`. This attaches the virtual disk image to the virtual Linux file system at the mountpoint `/mnt`.
+   6. Type `cp /mnt/vmware-linux-tools.tar.gz /tmp`. This copies the VMware Tools install program to the Linux file system in the `/tmp` directory.
+   7. Type `umount /dev/fd0`. The disk image is no longer needed.
+   8. Type `cd /tmp`. This moves you to the `/tmp` directory, and the prompt should change accordingly.
+   9. Type `tar zxf vmware-linux-tools.tar.gz`. This unpacks the VMware Tools programs to a new directory called (cleverly enough) `vmware-linux-tools`.

10. Type cd vmware-linux-tools. Apparently, they couldn’t think of anything shorter.

11. Type ./install.pl other. This installs VMware Tools.

> For most other distributions of Linux, do not include the word other: Simply type ./install.pl. If you install Linux-Mandrake in a virtual machine, use ./install.pl redhat.

12. The VMware Tools installer displays a summary of the work it is about to perform. Sample output is shown in Figure 10.14. Press Enter to proceed.

13. After the installation is complete, VMware should automatically detach the VMware Tools disk image and inform you that the virtual machine has returned to its normal state.

> Especially if you use your Linux VM in text mode, you might get complaints from VMware about how you haven’t installed VMware Tools yet. Ignore the later warnings. VMware Tools can’t just “uninstall” itself; it’s still there. It’s just that VMware does some primitive checking, and if it sees a text screen mode, it can get confused. You might want to turn off the notification if you use Linux virtual machines a lot.

14. In standard Linux distributions, you can proceed to configure and start X normally. In Corel Linux, you should reboot the machine. Type exit to quit the root account and reset the computer.

![](img/b2b6702758c230ce537468351fc8af15_199_0.png)

15. Corel Linux should boot to the standard KDE login screen, pictured in Figure 10.15. Log in using your normal username.

16. You see Corel Linux in beautiful, vibrant color! Any Linux distribution worth its salt should have come with a good variety of sample programs; load a few and enjoy your Linux virtual machine. Corel Linux automatically configures your virtual Ethernet card (bridged, host-only, or both) as well as the virtual sound card, if available (see Figure 10.16). In other Linux distributions, you might need to run the usual Linux configuration software to get these working.

![](img/b2b6702758c230ce537468351fc8af15_200_0.png)

Figure 10.15 After installing VMware Tools, Corel Linux can boot to a full-color display.

![](img/b2b6702758c230ce537468351fc8af15_200_1.png)

Figure 10.16 A basic Corel Linux OS desktop, with an extremely busy KDE theme.

17. Test the VMware Tools. Open a shell or terminal window and type vmware-toolbox & at the prompt. (The & detaches the process from the shell so you can enter other commands later.) If you do not run VMware Tools as root, you will not be able to access all its features. Use the su command if you feel the need to run VMware Tools as root.

## The Adventures of Screen Resolution in Linux Virtual Machines

Some of the concepts in this book are, I must admit, more than a little tricky. If you’ve made it this far, you’ve had to learn a lot. Get ready for something really confusing.

The VMware Tools XFree86 server inside a Linux virtual machine reads the settings of your host’s XFree86 server to come up with an optimum display size. This is all well and good. The problem comes when you want your Linux VM to have different display properties than your host PC.

In short, it’s tough. The guest XFree86 server starts out by exactly conforming to the specifications of your host’s XFree86 server. To make any changes, you will need to edit the file /etc/X11/XF86config.vm in your virtual machine.

Note that you cannot alter the color depth that the virtual machine runs in, only the resolution.

Open /etc/X11/XF86config.vm in a text editor, and scroll to the very last section, which should be introduced with

```
Section "Screen"
    Driver "accel"
```

You should see several lines starting with Modes, but only one will not have a # in front of it (indicating that it is uncommented, and the only line read by the guest’s X server at startup). Modify that line to include any screen resolutions you want to make available to the virtual machine. Be sure each entry is enclosed in quotes and separated by a space. They should be valid screen resolutions for your monitor and display card, preferably standard modes also in use by the host X server.

A line like

```
Modes "1024x768" "800x600" "640x480"
```

is functional and practical.
