# # LILO — Installation

To start SuSE Linux or any other operating system on your computer, you need a program to help you determine whether you want to use SuSE Linux or another operating system when starting (or booting) the machine. One such program is the boot manager LILO, the “Linux Loader”.\nBy default, YaST2 suggests installing the boot loader to the Master Boot Record (MBR) of the hard disk. If you have more than one hard disk, it will know which is used to boot by reading the BIOS settings. This is shown in the “suggestion screen” under “System boot”.\nYaST2 recognizes if you are operating systems other than SuSE Linux. Depending on the hardware, there are various ways to install LILO. The following provides you with an introduction to the LILO boot manager. A detailed description can be found in Chapter Booting and Boot Managers. When you select your LILO configuration by clicking ‘System boot’, the following dialog appears as shown in Figure 2.14.

![](bbox=[0.163, 0.438, 0.686, 0.703])

*Figure 2.14: LILO — Installation*

Decide in this dialog how and where to install LILO. There are four options for this.

+   1. To `/dev/hda` (in the MBR of your hard disk)\n2. Create boot floppy\n3. Do not install LILO (other boot manager)\n4. To another partition