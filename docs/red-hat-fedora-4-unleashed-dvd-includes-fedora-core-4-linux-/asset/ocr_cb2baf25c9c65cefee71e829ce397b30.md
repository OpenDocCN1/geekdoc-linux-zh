TABLE 2.2  Continued
| Item | Errata |
| --- | --- |
| Storage Device(s) | Removable: Size: Brand: Model: Controller(s): Rotational Speed: |
| Storage Device Controller Table | Type: Brand: Model: Interface: |
| Universal Serial Bus | Controller: BIOS MPS Setting: BIOS Plug-n-Play Setting: Device(s): |
| Video Device(s) | Brand: Model: Xinerama: Chipset: VRAM: |

Use the checklist in Table 2.2 as a general guideline for recording your computer's hardware and other capabilities. You can get quite a bit of information through hardware manuals or other documentation included with your PC, video, sound, or network interface card. Don't worry if you cannot fill out the entire checklist; Fedora will most likely recognize and automatically configure your PC's hardware during installation. Much of this information can be displayed by the dmesg command after booting. However, some of these details, such as your video card's graphics chipset and installed video RAM, can come in handy if you need to perform troubleshooting. You can also use the list as a post-installation check-off sheet to see how well Fedora works with your system.

# Preparing for the Install Process

The basic steps in installing Fedora are to plan, install, and configure. You'll need to decide on how to boot to an install and how much room to devote to Linux. Then perform the install (a sample step-by-step installation is in Chapter 3, "Installing Fedora") and afterward, configure your system to host new users and specific software services. Much of the initial work will be done during the install process because the installer, Anaconda, will walk you through partitioning, configuring the desktop, and configuration of any recognized network adapter.

There are many different ways to install Fedora Core, and selecting an installation method might depend on the equipment on hand, existing bandwidth, or equipment limitations.