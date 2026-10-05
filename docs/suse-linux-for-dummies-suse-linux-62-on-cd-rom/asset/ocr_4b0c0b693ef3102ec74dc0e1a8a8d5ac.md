# Chapter 5: Installation: Down to the Final Stretch

In most cases, you want to install LILO in the Master Boot Record. If you are using an alternate boot loader, then you might want to have LILO configured in the Boot Sector of the Root Partition.

+   **Boot Delay.** This is the number of seconds that the boot loader will pause before loading the default operating system. The default value of 10 seconds is a good choice and should be a long enough pause to give you a chance, during the boot sequence, to select any other boot options that you may.

+   **‘Linear’ Option.** This option is only used for less common hardware configurations and can usually be left blank. If you’ve used LBA mode to address SCSI disks with boot blocks 1023 cylinders, select the ‘Linear’ option. If you have turned on LBA mode in your BIOS and you are having difficulty installing LILO, you should select the ‘Linear’ option as.

+   **The following boot configurations are currently available.** Because this is your first time installing Linux, this list has no entries. Right? You can bring up the boot configuration screen by pressing F4.

The LILO Configuration dialog box prompts you for information that is required for each of the boot options (see Figure 5-26). The different configurations are described in the following list:

| LILO INSTALLATION | LILO (the Linux Loader) allows you to boot Linux from a hard disk. To |
| boot | LILO BOOT CONFIGURATION |
| confi | Please enter a label for this boot configuration,
| auto | which operating system it should boot, and the partition where
| confi | it is located. The label will be available for selection at the
| press | LILO prompt. When installing Linux, the boot configuration, you must also specify the location of the boot kernel. |
| Appen | Configuration name | :linux: |
| Where Which operating system | [Boot Linux] |
| | (Root-) partition to boot | [ /dev/hda2 ] |
| The f Kernel to be booted by LILO | :/boot/vmlinuz |
| are c Help F3-selection li |
| | < Continue | Abort >

![](bbox=[0.058, 0.555, 0.175, 0.638])

+   **Configuration name.** The configuration name is what you label. The name Linux is a good choice because most boot loader configuration examples use the label; it is descriptive. After you have entered the name, press Enter.

+   **Which operating system.** Select Boot Linux and press Enter.