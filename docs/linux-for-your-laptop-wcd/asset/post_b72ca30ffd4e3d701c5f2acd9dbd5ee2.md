
![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_159_0.png)

**Figure 5.20** *Enter your root password, along with other users for Linux.*

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_159_1.png)

**Figure 5.21** *Select the desired software packages to use with Linux.*

If you selected a Custom installation, you’ll see a list of software packages to use with Linux. You can scroll through the list, checking and unchecking packages. Click on the Next button to continue. You’ll see the window shown in Figure 5.22.

Scroll through the list of monitors and select one that matches your notebook’s display. You can try selecting an LCD panel or, if desired, try generic settings. When finished, click on the Next button. You’ll see the window shown in Figure 5.23.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_160_0.png)

**Figure 5.22** Select your monitor for X11.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_160_1.png)

**Figure 5.23** Select the X11 server to use with Linux during X11 sessions.

Scroll through the list of servers to use during X11 sessions on your laptop. Click on a button to set the amount of video memory provided by your notebook. You can test the settings. Then—and only then—you should select the Use Graphical Login item. Note that this dialog box will be different in newer versions of Red Hat's installation when XFree86 4.0 becomes part of most Linux distributions! When finished, click on the Next button. You'll see the installation dialog box, as shown in Figure 5.24.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_161_0.png)

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_161_1.png)

If you're sure you want to install Linux, click on the Next button to begin the installation. You'll see the dialog box shown in Figure 5.25.

You'll see a progress dialog box as Linux is installed. This process can take from 15 minutes to an hour, depending on your software selection and the speed of your notebook's CD-ROM and hard drive. When all the software is copied from

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_161_2.png)

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_161_3.png)

CD-ROM, the Red Hat installer will ask you to click on an Exit button or press Enter to reboot your notebook.

## Logging In and Shutting Down

When you first log in, enter `root` or your username and press Enter. Next, type in your root or username's password. You can also shut down or reboot Linux using the X11 graphical login. To shut down your notebook from Linux, use the `shutdown` command with its `-h (halt)` option:

```
# shutdown -h now
```

To reboot Linux from the command line of the console or an X11 terminal window, use the `shutdown` command with its `-r (reboot)` option:

```
# shutdown -r now
```

## Installing Yellow Dog Linux

Installing Yellow Dog Linux on the iBook is easy. Using Yellow Dog Linux (which is based on the Red Hat file system) is a lot of fun and a great way to learn Linux. After preparing your iBook's hard drive for Yellow Dog Linux, boot to the newly installed Mac OS, insert your Yellow Dog Linux CD-ROM, and install the BootX control panel to your iBook's System folder. (One component, BootX App, goes to the Control Panel folder, and the other component, BootX Extension, is placed in the Extensions folder.)

Next, copy the files `vmlinuz` and `ramdisk.image.gz` from the CD-ROM to your iBook's System folder. Start the BootX control panel, select the `vmlinuz` Linux kernel, and click on the No Force Driver option. Click on the BootX Options button, and then select the Video video settings item. Next, click on the Use specific RAM disk button, and then click on the Choose button to select the `ramdisk.image.gz` file. When finished, click on the OK button.

If you choose to use a single Linux native partition on your iBook, this partition will be designated `/dev/hda10`. Therefore, in the main BootX dialog box, enter `hda10` for the root device. This designates the root Linux partition. Next, enter `adb_buttons=103,11` in the More kernel arguments: field. This designates F11 and F12 as the middle and right mouse buttons for the iBook's single-button ADB mouse. Click on the Save to pref button to finish your configuration.

Make sure the Yellow Dog Linux CD-ROM is inserted in your iBook, and then click on the Linux button in the BootX dialog box to start the installation.

The installation of Yellow Dog Linux proceeds along the same lines as a text-based Red Hat Linux installation. However, you’ll need to do the following:

-   Configure and format a swap partition.
-   Configure and format a root Linux partition (which should be /dev/hda10).
-   Configure the iBook mouse as a single-button ADB mouse.
-   Configure the iBook’s internal Ethernet interface (if desired).

After installing Yellow Dog Linux, log in as the root operator, and edit the system’s initialization table, /etc/inittab:

```
# pico -w /etc/inittab
```

Change this entry:

```
id:3:initdefault
```

to this:

```
id:5:initdefault
```

Save the file (press Ctrl+X) and exit the editor. This will configure Yellow Dog Linux to boot directly to an X11 session. Here are some things to keep in mind about Yellow Dog Linux on the iBook (these points were true at the time this chapter was written):

-   You must use the same color depth settings and resolution for the Mac OS and Linux (800×600 at 16bpp, or thousands of colors).
-   The internal Ethernet port works, but it does not respond well to being placed in “up” or “down” status using the ifconfig command.
-   The current Linux kernel for the PowerPC chip does not enable sound on the iBook.
-   The iBook’s internal modem does work with Linux, but you must boot Linux using the Yaboot boot loader and Apple’s Open Firmware boot prompt. However, your X11 sessions will be limited to 256 colors. Browse to http://www.yellowdoglinux.com/support/ff\_bootloader.shtml for a discussion on using the Yaboot utility.

Hopefully, these issues will be resolved in the near future; development of PPC Linux is quite active, and new features are continually being added. Chances are quite good that iBook users will enjoy the full benefits of Linux in only one or two more revisions of the Yellow Dog Linux distribution.

## Resource Information

http://www.serv.net/~sand/hurd/partitions.html

An interesting diatribe on partitioning, including a discussion of BSD UNIX.

http://www.users.intercom.com/~ranish/part/primer.htm

A great graphical introduction to partitioning.

**Linux Installation-HOWTO**

Eric S. Raymond's must-read for first-time Linux installers. Section 6.4 discusses the basics of partitioning. It can be found under the /usr/doc/HOWTO directory or at http://www.linuxdoc.org.

**Linux Partition-HOWTO**

Kristan Koehntopp's planning guide for partitioning before and after installing Linux. It can be found under the /usr/doc/HOWTO/mini directory or at http://www.linuxdoc.org.

http://www.powerquest.com/usindex.html

PowerQuest's home page, with links to PartitionMagic.

http://www.igd.fhg.de/~aschaefe/fips/

Arno Schaefer's FIPS home page. This is the definitive place to go for the latest version of this free DOS-based partitioning tool.

http://www.mklinux.org/getting_started/preparations/HDDSetup.html

A step-by-step introduction to using Apple's HD SC Setup to prepare a drive for Linux.

ftp://c3po.terraplex.com/pub/terrasoftsolutions/yellowdog/guide_to_install/

A directory holding 144dpi and 72dpi versions of the Yellow Dog Linux 1.2 installation guides in Adobe Acrobat format.

# Chapter 6: Post-Installation Issues

Using a Boot Manager
PCMCIA and Card Services
Configuring Sound
Solving Problems with X
Resource Information

This chapter provides potential solutions and troubleshooting information you can use if you have problems after installing Linux. Installing Linux for the first time on a new notebook is an exciting experience, made even more pleasurable when Linux is configured to work with all your notebook's components. However, notebook manufacturers use a wide variety of chipsets and hardware in notebook lines, so you might have to spend time tracking down and fixing problems with your installation.

Here are the main areas of concern when you're configuring Linux on a notebook:

-   **Booting**. Ensure that LILO or your boot procedure works properly. If you configure a dual-boot system, you should be able to boot to either installed operating system between a system restart or shutdown.
-   **X.** The X Window System should be configured to provide the optimum resolution and color depth available for your notebook. Pointer devices, such as trackpads and erasers, should work properly.
-   **Sound.** The Linux kernel modules or other software should enable you to play audio CDs, MIDI files, or .mp3 files through your notebook's sound system.
-   **Networking.** You can use your notebook's built-in or PCMCIA Ethernet adapter to access your local LAN or a remote network.
-   **Modem and serial ports.** You should be able to access your notebook's serial port(s), perhaps use IrDA, and configure either an internal or external modem.
-   **Printing.** The printing software included in your Linux distribution should work properly with your printer(s).

The important thing to remember is that nearly all Intel-based notebooks run Linux and can be configured to provide capabilities that match the laptop's hardware. You'll have a much better chance of configuring your notebook if it has been on the market for at least a year and is not the latest and greatest model from the manufacturer. This is because manufacturers generally upgrade internal components, such as video chipsets and sound systems, to provide new features but are loath to share technical specifications. Since few (if any) chipset makers or notebook manufacturers have hopped on the Open Source bandwagon, Linux developers are often denied access to critical information needed to make video or sound drivers work with the newer hardware. Hopefully, this situation will change as more consumers demand open specifications and hardware that will run Linux.
