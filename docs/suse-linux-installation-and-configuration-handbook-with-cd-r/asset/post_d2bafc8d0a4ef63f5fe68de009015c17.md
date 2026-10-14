
# CAUTION

On some old systems, the BIOS was unable to see past cylinder number 1024 of the hard disk. Because LILO uses the BIOS to load the operating system, if the operating system was placed after cylinder number 1024, LILO would fail to boot it. Therefore, you might need to create a separate partition for /boot somewhere before cylinder number 1024. The /boot directory contains all the files required to boot Linux. Thus, by placing it before cylinder 1024, you should have no problems booting Linux. After Linux boots, you don't have to worry about that BIOS problem anymore. Please note that this problem exists in old hardware and if you have a Pentium class PC and up, chances are great that you don't have that limitation. However, if you need to use any BIOS extension software, you will likely experience this problem. In that case, you will need to consult your hard disk manufacturer to obtain these BIOS extensions. Another solution of course is to try and place your installation before the 1024 cylinder.

The next option, the Boot Delay, is the number of seconds that LILO should wait before proceeding to execute the first boot configuration. You can have LILO wait for you to pick an operating system to load, and then when it times out, it will load the first operating system on its list.

The Linear option is a fix for a problem with the BIOS not being able to handle disk geometry gracefully. Setting Linear to on can avoid problems caused by the BIOS.

The last option lists all the boot configurations that are currently available. The first one on the list is the default.

## Adding a New Boot Configuration to LILO

To have LILO boot an operating system, you need to add it to the list of boot configurations. This is easy to do once you have all the information you need. This information depends on the boot configuration that you are trying to build. You can use LILO to either boot a different kernel for your SuSE Linux system, or load a different operating system altogether.

You might want to have LILO boot a different kernel for your installed Linux system for testing purposes. For example, say you installed a new kernel and you want to test it before you actually use it as your default. In this case, you can use LILO to load it upon demand. All you will need to know is the full path of the new kernel.

If you want to use LILO to load a different operating system, you will need to know on what partition that operating system lies. For example, if you have Windows 98 installed on your machine along with Linux, you need to know where Windows is installed. This is easy to do using fdisk—follow these steps:

- 1. Log in as root.
- 2. Open an X terminal if you are using the X Window System.
- 3. Start fdisk, passing your hard disk as a parameter:

```
# fdisk /dev/hda
```
- 4. Type p to have fdisk show you all the partitions on your hard disk.
- 5. To find where Windows is installed, you should use a line such as this:
- `/dev/hda2 256 1997 13992615 f Win95 Ext'd (LBA)`
- From the file system type at the end of the line, you can tell that this is a Windows 9x partition.
- 6. Now that you know the partition you want is /dev/hda2, type q to quit fdisk.
- You can use LILO to boot this partition.

> TIP
> 
> You can use LILO to boot another installation of Linux. Yes, you can have another partition with SuSE Linux on it and have LILO boot it. In this case, you will need to know the name of the partition on which this second SuSE Linux installation lies. Why would you want to do this? If you want to test something and you are too worried you might corrupt your main SuSE Linux installation, you can have another one to test.

Now that you have the information you need, you can create a new boot configuration for LILO:

- 1. Run YaST in the LILO configuration mode:
- `# yast --mask lilo`
- 2. Press F4 to add a new configuration for LILO to load.
- 3. In the Configuration Name option, type the name you want to use to load this configuration. For example, if this configuration is going to load Windows 98, a good name might be win.
- 4. Press the Tab key to move on to the Which Operating System option. Here you have three choices from which to pick:
  - **Boot Linux**—Choose this option if you want to boot another kernel for your system.
  - **Boot DOS/Win**—Choose this option if you want to boot a Windows- or DOS-based partition. This option should be used if you want to boot any other operating system, including another Linux partition.
  - **Boot OS/2**—Choose this option if you want to boot OS/2.
- 5. The next option is (Root) Partition to Boot. This is where you specify to LILO the partition to boot. YaST will attempt to guess the correct partition to boot according to what you picked for an operating system. Correct it if it's wrong. (To see a list of partitions that fit your operating system choice, press F3.)
- 6. The Kernel Optional option is activated if you pick Boot Linux. This option is useful if you are testing a new kernel. When you check this option, LILO will never complain if it can't find the test kernel.

7. The Kernel Optional option again is only activated if you choose Boot Linux. This is where you tell LILO the exact path to the kernel it should boot. Press F3 to get a window with a list of all the directories that you have on your hard disk. Navigate to where your kernel is and press Enter to pick it. The default kernel location is the /boot directory if you used a SuSE pre-compiled kernel, whereas it is the / directory if you downloaded and compiled a new kernel.

8. Press Tab to highlight the Continue button and press Enter to save your boot configuration.

9. YaST returns to the LILO Installation window—notice how your boot configuration was added to the list. Figure 9.2 shows the boot configuration setup by YaST.

### FIGURE 9.2
New boot configuration added to LILO setup in YaST.

![](img/659f91d9da7b29976c0625e2e9628511_215_0.png)

10. Press Tab to highlight the Continue button and press Enter to save this configuration to LILO.

11. YaST runs LILO to apply the changes. The result of the operation is shown in a small window. Figure 9.3 shows a successful LILO installation message.

### FIGURE 9.3
YaST runs LILO to install a new MBR. The result is either a success or failure. In all cases, YaST will tell you the result.

![](img/659f91d9da7b29976c0625e2e9628511_215_1.png)

12. Press Enter to quit.

> **TIP** When you download a Linux kernel and recompile it, the kernel is installed in the root directory (`/`) by default. However, you might want it to be installed in the `/boot` directory. To do so, you just have to edit the makefile of the kernel and change the line that says:
> 
> `INSTALL_PATH=/`
> 
> to
> 
> `INSTALL_PATH=/boot`
> 
> This way, when you compile and install the new kernel, it will be installed in the `/boot` directory.

## Editing and Removing a Boot Configuration

If you want to edit one of the currently available boot configurations, you can do so using YaST. Follow these steps:

- 1. Run YaST, entering the following command:
  `# yast --mask lilo`
- 2. Use the Tab key to move to the list of available boot configurations.
- 3. Select the one you want to edit.
- 4. Press F5 to edit it or F6 to remove it.
- 5. When done editing, press Continue to exit.
- 6. Press Continue to save and quit.

## Advanced LILO

YaST is perfect if you want to quickly configure LILO's most common options. But LILO has more options than YaST shows, and the only way to set those up is by directly manipulating LILO's configuration file—`/etc/lilo.conf`. A common LILO configuration file is made up of two sections.

The first section is the Global section, where you put all the options for LILO, as well as any options that apply to all the boot configurations.

The second section is the Boot Configurations section, where you have the settings for all the boot configurations. You can give each configuration its own set of options that apply only to it.

A basic lilo.conf file looks something like this:

```
# Start LILO global Section
boot=/dev/hda
#compact    # faster, but won't work on all systems.
vga=normal
read-only
prompt
timeout=100
# End LILO global Section
other = /dev/hda1
```
