+   - Enter expert at the boot: prompt to perform the installation and upgrade in an expert user mode. In expert mode, the Red Hat installation program does not try to auto-detect your hardware, but instead allows you to select various hardware components manually. You should choose to enter expert mode only if you really are an expert or are having problems with auto-detection of certain hardware.

+   - Enter rescue at the boot: prompt. Use this option when you are trying to recover from a disaster. In such a case, you need a rescue disk along with your standard boot disk. You can create the rescue disk in the same manner as you create the boot image disk or the supplementary image disk. Just replace the image filename with rescue.img in any of the boot image creation processes described previously.

![](bbox=[0.1, 0.5, 0.2, 0.65])

**Tip**
If you plan to perform an unattended installation, where user interaction is not required, you can also enter linux ks at the boot: prompt. This allows the installation program to use an installation mode called the Kickstart mode. This is a very advanced mode that requires that you create a custom configuration file called ks on the boot floppy disk or keep a file called <IP address of the machine being set up>kickstart in the bootp server.

Assuming that this is your first time Red Hat Linux installation, your only choice is to press the Enter key to start the installation process. When the installation program starts, you see another welcome screen. Press Enter to continue with the installation.

# Selecting a language, a keyboard, and an installation method

After you are past the initial greeting page, you are asked to choose the language you want to use; the default is English. Choose the appropriate language and press Enter to continue. The next screen asks you to select a keyboard type. The default is English. Press Enter or select the appropriate keyboard type and continue. Next, you are asked to choose an installation