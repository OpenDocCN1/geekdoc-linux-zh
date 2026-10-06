Those options are:

+   - Boot Device. The hard drive on which LILO will write its information, and the choice of using the either Master Boot Record (in this case /dev/hda) or the boot record of a partition (for example, /dev/hda1). You can write LILO to a partition if you like some other boot loader program to control the Master Boot Record.

+   - Boot Map and Install To are internal configurations of LILO, and should not be changed.

+   - Message allows you to insert a message that is seen when LILO starts.

+   - Password allows you to add a password to LILO.

+   - Timeout is in seconds before the default boot image is executed.

+   - Verbosity defines the amount of information LILO gives to the administrator when it is writing to the drive. The scale is from a low of 0 to a high of 5, and the information is only shown if the LILO command is issued from a command line. You will not need any additional information if you use turboscfg.

+   - Append allows you to add extra parameters to the kernel. Some configurations may need extra parameters to start devices.

+   - VGA resolution choices are 80x25 or 80x50, or you can require the choice to be at boot time. Note that "at boot" offers a few other choices.

The other options on this window are beyond the scope of this book. If you need more information on them you can read the LILO HOWTO as

http://www.linuxxdoc.org/HOWTO/mini/LILO.html

# 5.7 Determining your hardware

There are several ways you can determine your hardware. These methods include:

+   - Boot messages. The file /var/log/messages is a plain text file containing the boot messages. The system will attempt to find hardware devices when you boot up. It may recognize the hardware devices and then attempt to use modules that are compiled in the kernel or modules that are loaded separately. Sometimes the system will recognize the hardware but will be unable to load the modules due to some hardware or setup inconsistencies or version dependencies.