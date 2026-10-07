# The Linux Kernel

787

file contains the scripts that make how to manipulate the source code and associated files; you will not have to edit this file. You can use your favorite text editor, however, to edit the other file by changing the EXTRAVERSION line (near the top of the file) to give your kernel a unique version number.

We've already discussed the contents of the config subdirectory, so let's examine the other directories found under /usr/src/linux-2.4. The most useful for us is the Documentation directory, and in its subdirectories, you will find all the documentation concerning every part of the kernel. The file 0-INDEX (each subdirectory also contains a 0-INDEX file as well) contains a list of files in the main directory and a brief explanation of what they are. Many files are written solely for kernel programmers and writers, but a few are useful to the intermediate or advanced Linux user when attempting to learn about kernel and device drivers. Some of the most interesting and useful documents

devices.txt—List of possible Linux devices that are represented in the /dev/, giving major and minor numbers and a short description. If you have ever gotten an error message mentioning "char-major-xxx", this file is where that list is kept. Devices are mentioned in Chapter 10, "Managing Filesystems."

ide.txt—If your system uses IDE hard drives, this file discusses how the kernel interacts with them and lists the various kernel command that can be used to solve IDE-related hardware problems, manually set data transfer modes, and otherwise manage your IDE drives. Most of this management is automatic, but if you want to understand how the kernel interacts with IDE devices, this file explains it.

initrd.txt—Chapter 10 also discusses the initial ramdisk. This file provides much more in-depth knowledge of initial ramdisks, giving details on the loopback filesystem to create and mount and explaining how the kernel interacts with them.

kernel-parameters.txt—In Chapter 7, "Managing Services", we touch briefly on kernel arguments, which are commands that can be passed to the kernel at boot to configure kernel or hardware settings. This file is a list of most those kernel arguments, but it doesn't appear too useful at first glance because it's a list. However, knowing that a parameter exists and might relate to what you're looking for can assist you in tracking down more information than you have to enter into an Internet search engine like http://www.google.com/linux.

sysrq.txt—If you have ever wondered what key you keyboarded "SysRq" was used for, this file has the answer. Briefly, it's a key combination hardwired into the kernel that can help you recover from a system lock. Red Hat disables this by default for security reasons. You can re-enable it by entering the command # echo "1" > /proc/sys/kernel/sysrq and disable it by choosing a value of "0" instead of "1"

In the nearly 30 other directories found in Documentation, you'll find similar text files that deal with the kernel modules for CD-ROM drivers, filesystem drivers, gameport and

![](bbox=[0.925, 0.355, 0.995, 0.405])