# Chapter 1

+   *   **Video (graphics) card**: Note the chipset of the video card and the amount of RAM. While the Red Hat X-server configuration program can usually probe and detect the video card, it sometimes fails. If it does fail, you'll need to tell Red Hat Linux the name of your video card chipset. Note that the video RAM is sometimes also displayed on the computer screen during boot up of the machine.

> If you can't find the name of your video card chipset in the Hardware Compatibility List (see below), don't worry. Note that this means only that the GUI of Red Hat Linux is affected. Generally, if you intend to use the computer only as a server system, you're recommended not to install any GUI — this is for reasons of resource load and security. If you do want a GUI, you'll still be able to configure your machine to use the VESA interface for running the X-server. The VESA interface standard is supported by most of the commonly available video cards.

+   *   **Monitor**: If you have an unusual monitor model, then the configuration of the GUI X Server software (during the installation process) might not detect it. Therefore, it's worth noting information regarding your monitor. You'll need the horizontal and vertical sync rates, which can generally be found either in the monitor manual or at the monitor manufacturer's web site.

+   *   **Sound card**: While the installation tries to detect the sound card, it sometimes doesn't succeed. Therefore, it's good to note the name of the sound card chipset in advance.

+   *   **Network card**: During installation, Red Hat Linux tries to detect the network interface card (NIC) and load the appropriate software driver automatically. You should note the name of the chipset of the NIC in advance of installation, just in case the installation process fails to determine it.

How do you get hold of this information? Well, if you have the technical specification documents that were supplied with your computer, then you'll find the information in there. If not, then the machine's existing operating system will probably offer some way of browsing the hardware being used. For example:

+   *   In Windows 2000, you can find out about existing hardware via Start | Settings | Control Panel | System (select the Hardware tab, and click the Device Manager button).

+   *   In other Linux systems, you can find out about existing hardware through via various menu options of the GUI. For example, try the options in Programs | Settings or Main Menu | System Tools, depending on which version of Linux you're using.

# The Hardware Compatibility List

Red Hat maintains a list of officially supported hardware, called the Hardware Compatibility List (HCL). The HCL lists all the hardware components against which the operating system has been checked extensively for proper functioning. The list is available at [http://hardware.redhat.com/hcl/](http://hardware.redhat.com/hcl/).

16