any point before the system warns you it is about to write to the hard disk (or you complete the installation). If you opt out before this point, the system is left in its original state. The R\&M disks also allow a system booted from a live CD to leave the hard disk untouched.

+   5. You can check the installation media at this point.

+   6. The Anaconda installer prompts you with a few questions about how you want to configure Fedora/RH\&M, probes the hardware, starts the X Window System for a graphical installation, and then collects more information about how you want to install Fedora/RH\&M.

+   7. When Anaconda is finished collecting information, it writes the operating system files to the hard disk.

+   8. When you reboot the system, Firstboot asks you questions that are required to complete the installation (page 66).

+   9. The Fedora/RH\&M system is ready to use.

# ## The Medium: Where Is the Source Data?

When you install Fedora/RH\&M, you copy operating system files from a source—frequently a CD/DVD—to the target computer's hard disk. The files that hold the data you use to burn a CD/DVD are called _ISO image files_. They are named for the standard that defines how the data is stored (ISO 9660). There are several sources for these files.

# ### CD or DVD

Red Hat Enterprise Linux DVDs are sold by Red Hat and its distributors. ISO image files for Red Hat Enterprise Linux are available by subscription from Red Hat Network. You can download a 30-day evaluation copy of RH\&M from the Red Hat Web site. See also “Checking and Burning the CD/DVD” (page 45).

This book includes the DVD necessary for installing Fedora (the install DVD). Alternatively, you can purchase a Fedora CD/DVD from third-party vendors or you can download a Fedora ISO image file and then either install from the image or burn a CD/DVD (next section).

# ### Hard Disk

You can store ISO image files on the target system's hard disk if it is already running Linux. You can use the first installation CD, the Net Boot CD, the install DVD, or a USB flash drive to boot the system for a hard disk installation. See *asmkmethod* on page 70 for more information. Alternatively, you can use a preupgrade (page 30) to install from the hard disk of a system running Fedora.