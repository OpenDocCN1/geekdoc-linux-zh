# 9 Optimizing your Virtual Machine Environment

This chapter contains useful tips for optimizing the performance of your virtual machine, and to make your virtual environment easier to work with.

# 9.1 Performance Tips

A few basic tips can help you experience better performance in your virtual machines. First, make sure that you always install the VMware tools (especially for Windows), because together with the SVGA display driver, the performance with using the guest operating system is much better.

+   - Disconnect the CD-ROM device

If your guest operating system is trying to access the CD-ROM or DVD player, (either because you inserted a CD-ROM, or because the OS or an application is trying to read data from a CD-ROM that is not there), that process could slow down the host and guest.

When your virtual machine is completely configured and the OS is installed, go to the virtual machine settings and set the CD-ROM device not to Connect at power on.

![](bbox=[0.48, 0.4, 0.92, 0.82])

Figure 9.1: Configure CD-ROMs as not connected by default.

+   - Run in full screen mode

In Windows, but especially in a Linux host working in the graphical environment is much faster if you run your virtual machine in full screen mode.