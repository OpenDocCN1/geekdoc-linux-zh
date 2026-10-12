
- Pressing **F3** gives general installation information (described next in this chapter).
- Pressing **F4** describes how to pass kernel video arguments, useful for configuring video hardware to support a graphical install at a specific resolution (such as 800 × 600 pixels).
- Pressing **F5** describes Fedora's rescue mode.

![](img/774d40fd20903495c5cd00e2efad3f33_96_0.png)

FIGURE 3.1 Select an installation option in this first Fedora Core boot screen.

Some of the options you can use at the boot prompt include:

- `linux noprobe`—Disables probing of the system's hardware.
- `linux mediacheck`—Verifies the integrity of one or more install CD-ROMs.
- `linux rescue`—Boots to single-user mode with a root operator prompt, disabling X, multitasking, and networking; this option can be used if you need to reconfigure your boot loader or to rescue data from your system.
- `linux dd`—Uses a driver disk (a floppy image) and possibly one or more kernel arguments (such as `linux mem=512M expert`) to enable certain types of hardware, such as networking cards.
- `linux askmethod`—Prompts for the type of install to perform, such as over a network.
- `linux updates`—Starts an installation update.
- `memtest86`—Starts a cyclical, intensive series of memory tests of your PC's RAM.
- `linux nofb`—Starts a graphical installation, but does not use a framebuffer (helpful with problematic or unsupported video).
- `linux resolution=width × height`—Installs using a graphical display of width-by-height pixels (such as resolution=800×600), which can help match older or less capable display monitors and video cards.

The F4 screen lists options that can be used at the boot prompt to set a specific resolution for the installation. For example, this is done by typing `linux resolution=` at the boot prompt, along with an option such as "800×600". Other options, such as optional arguments for kernel modules (in order to properly configure or initialize hardware) may be passed to the install kernel if you use the `noprobe` option.

> **TIP**
>
> The installer will start automatically in 60 seconds. Press the spacebar, reboot, or turn off your PC if you need to halt the install.

After you press Enter, the installer’s kernel loads, and you’re asked (in a text-based screen) if you would like to perform a media check of your CD-ROM, as shown in Figure 3.2.

This check can take quite some time (depending on the speed of your CD drive), but can ensure the integrity of the CD-ROM’s contents, as an md5sum value is embedded on each CD-ROM. This check can help foil installation of malicious software from CD-ROMs with tampered contents. The check can also be helpful to make sure that the CD-ROM you are using will work on your PC and in your CD drive. To perform the check, choose OK; otherwise, use the Tab key to navigate to the Skip button and press Enter to choose it.

![](img/774d40fd20903495c5cd00e2efad3f33_97_0.png)

FIGURE 3.2 You can check your CD-ROM media before installing Fedora.

After checking your CD-ROM or skipping the check, the display will clear. The Fedora installer, Anaconda, will load, and you are presented with a graphical welcome screen as shown in Figure 3.3. The installer should recognize your PC's graphics hardware and mouse. You can then click on the Release Notes button to get detailed information about Fedora Core, along with tips on hardware requirements and how to perform various installs.

If your pointing device (mouse) is not recognized, you can press Alt+R to “press” the Release Notes button. Similarly, you can click Alt+H to hide text shown on the left side of the screen, but you should take a minute to read the frame’s contents.

![](img/774d40fd20903495c5cd00e2efad3f33_98_0.png)

**FIGURE 3.3** Read Help or Release Notes before installing Fedora.

Click Next (or press Alt+N) to continue, and the installer asks you to select one of 31 different languages for the installation, as shown in Figure 3.4.

You can navigate the installer's dialogs (during a text-based or graphical install) using the Tab key. You can scroll through lists using your cursor keys. Note that you can now “step backward” through the install by using a Back button. Select a language and click the Next button.

You’ll then be asked to select a keyboard for the install, as shown in Figure 3.5.

Scroll to the appropriate keyboard option. You use this option to configure the install to support one of 53 different language keyboards. Click Next after making your selection.

![](img/774d40fd20903495c5cd00e2efad3f33_99_0.png)

**FIGURE 3.4** Select a language to use when installing Fedora.

![](img/774d40fd20903495c5cd00e2efad3f33_99_1.png)

**FIGURE 3.5** Select a default keyboard to use when installing and using Fedora.

If your PC's monitor was not detected, you might be asked to select your model from 132 different manufacturers. In rare instances, you might have to specify your monitor's exact horizontal and vertical frequencies. This can happen with older displays.

If an existing Linux install is detected, you'll be asked if you want to upgrade and reinstall; otherwise, you're then asked to select a type of installation, as shown in Figure 3.6.

![](img/774d40fd20903495c5cd00e2efad3f33_100_0.png)

**FIGURE 3.6** Select a type of installation.

Select a type of installation suitable for your intended use—we’ll use a Server install for our example. As we mentioned earlier, you can use the Custom install instead to select the specific packages to be installed. This can be helpful in order to prune unnecessary software from your system and might save some time later on. After you select the installation type, click **Next** to continue. You will then see a screen that offers a choice of partitioning schemes and tools.

> **NOTE**
>
> Fedora’s installer also supports the ability to monitor background and install processes running during an installation. You can watch the progress of an install and hardware information reported by the Linux install kernel by navigating to a different console display or virtual console by simultaneously pressing the Ctrl, Alt, and appropriate Fn key (such as F1–F5).
>
> Use this approach to watch for kernel messages, monitor hardware detection, gain access to a single-user shell, and view the progress of the installer script.
>
> When using a graphical installer, press Ctrl+Alt+F4 (then Alt+F2 or Alt+F3) to navigate to the various screens. Press Alt+F7 to jump back to the installer. When performing a text-based installation, use Alt+F2 (then Alt+F3 or Alt+F4). Use Alt+F1 to jump back to a text-based install.

### Partitioning Your Drive

You learned how to choose and plan a partitioning scheme in “Planning Partition Strategies,” earlier in this chapter, based on the more specific partitioning information offered in Chapter 2. The Disk Partitioning Setup screen, shown in Figure 3.7, offers two options for disk partitioning. Here is what the options do:

- Using the Automatically Partition button conveniently partitions your hard drive according to the type of installation you selected and configures the partitions for use with Linux.
- Choosing the Manually Partition with Disk Druid button launches a graphical partition editor that enables the creation of custom partition schemes.

![](img/774d40fd20903495c5cd00e2efad3f33_101_0.png)

FIGURE 3.7 Select a partitioning scheme or tool.

> > **NOTE**
> >
> > See the section “Partitioning Before and During Installation” in Chapter 2. Chapter 10, “Multimedia Applications,” contains information on using another partitioning utility, the text-based Linux `fdisk` command.

For this example, select Manually Partition with Disk Druid button and click Next. If you are using a new hard drive that hasn’t previously been partitioned, you will be asked if you would like to create new partitions on the drive. Click the Yes button to initialize the drive. If you are using a hard drive that has been previously partitioned or formatted and the partitions are recognized, Disk Druid will present the partitions in its partition dialog. Figure 3.8 shows the graphical interface presented for a 6GB hard drive that hasn’t been partitioned.

To use Disk Druid, select any listed free space, and then click the New button (or press Alt+W) to create a new partition. Alternatively,

- To get help, see the help frame on the left.
- To create free space, scroll to an existing partition and use the Delete button to delete the partition.
