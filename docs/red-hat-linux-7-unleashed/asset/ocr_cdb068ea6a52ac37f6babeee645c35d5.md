The main thing to remember is that if you require PCMCIA support to install Linux, you will need a support disk.

Here’s a checklist that you can use to see if you’ll need to create a PCMCIA support disk:

+   - Installing from a PCMCIA-Connected CD-ROM-If you’ll be installing Red Hat Linux from a CD-ROM, and your CD-ROM drive is attached to your computer through a PCMCIA card, you’ll need a support disk.
+   - Installing using a PCMCIA Network Card-If you will be using a PCMCIA network adapter during the installation, you’ll need a support disk.
+   - If you have determined you will need a support disk, you will have to make one. The PCMCIA support disk image file is pcmia.img, and is located in the images directory on the first Red Hat Linux CD.

Check out “Creating Boot Disks” earlier in this chapter. It will inform you on how best to create these disks and which kind is best for your system.

# # Step-by-Step Installation

This section takes a step-by-step look at the CD-ROM installation process. It will guide you through the install step by step and help you along the way. It will also inform you on the preferred options to select and why you should select them.

# ## Starting the Installation

The best way to start your installation is to check and see if your BIOS supports booting from the CD drive. Most computers built after mid-1997 have this option. On boot you will see a line of text telling you to press either the F1 or the Delete key to enter the BIOS settings and change the boot order so that the computer can boot from the CD drive. Save these settings and reboot the machine. The computer will then boot from the CD drive. When the install is finished, change your settings back to the way they were. If your computer doesn’t support this, create and boot off a boot disk.

> **Caution**
> If you change the BIOS setting regarding your hard drives, it can have adverse effects on your system.