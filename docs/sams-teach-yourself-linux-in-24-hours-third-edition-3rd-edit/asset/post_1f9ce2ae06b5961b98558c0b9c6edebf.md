
## Working with the X Window System

Configuring the video display is probably the most difficult part of a Linux installation. There are so many variables to consider—the monitor, the video card, screen resolution, color depth, and refresh rates. If you run into problems adjusting the video, consider setting up a simple SVGA monitor at 800x600 resolution with 256 colors. When you have this minimal display, you can begin adjusting one video setting at a time until your screen looks just the way you want.

## Adding Networking and Internet Access

One downside you might find in the Linux world is the lack of plug-and-play support. Although there are efforts underway to increase plug-and-play capabilities in Linux, compatibility might become a problem when it comes time to connect to the Internet. Most internal modems, and all Winmodems, are not compatible with Linux. If you are having problems getting Linux to recognize the modem, you might want to consider hooking up an external modem to the computer.

## Playing Games

There is growing interest in Linux games. You'll find the old standard, low resource usage games such as Solitaire, but you won't find fun and excitement there. Many games for the Microsoft Windows operating system are being developed for Linux. There is a growing list of games that have already been ported to Linux. Also, there are DOS and Windows emulators that will permit you to run games written for those operating systems. Many Linux enthusiasts have taken to the Internet and the multiplayer games. Just remember, games require heavy-duty video and sound capabilities. Make sure that Linux supports drivers for your 3D-accelerated video card, stereo sound system, and joystick.

## Determining Hardware Compatibility

The best way to configure Linux properly and to avoid surprises during the installation is to collect as much information as you can about the hardware installed on your computer. This is when the manuals packaged with the hardware come in handy. To set up the video display properly, it's always a good idea to get out the manual for the monitor. If you don't have the hardware manuals, call the vendor (or check their Web site) to see whether you can get replacements. Hardware information can also be found by searching through the computer itself—by asking the already installed operating system to display the system properties.

Each Linux distributor posts on its Web site a list of hardware that is compatible with its Linux distribution. Another resource that lists the computer hardware that is compatible with Linux in general is the Linux Hardware Compatibility HOWTO (also referred to as the Hardware-HOWTO).

To determine whether your computer hardware is compatible with the Linux operating system, take an inventory of the devices attached to the computer and collect system information about each device. Table 1.2 lists the devices that you'll need to inventory and the type of information you'll need for each device. After you have collected this information, you can compare your list with the Linux Hardware Compatibility HOWTO.

## Table 1.2 Collect System Information for Each Device Attached to the Computer

| Device Type | Required System Information |
|---|---|
| Hard drives | Number of drives attached to the computer, whether they are IDE or SCSI drives, the size of each drive (in MB), partitions, space allocated for Linux |
| CD-ROM drives | Interface type (either IDE or SCSI), manufacturer, and model number |
| RAM memory | Amount of RAM installed on the system |
| Serial ports | Number of serial ports, port assignments (COM1, COM2), IRQ addresses |
| Parallel ports | Number, port assignments (lp1, lp2), IRQ |
| SCSI adapters | Manufacturer and model number |
| Network cards | Manufacturer, model, number and chip set |
| Modem | Manufacturer and model number, speed, communications port (COM port), fax support |
| Mouse | Type of mouse (bus, PS/2, or serial), number of mouse buttons, port attached to, the mouse protocol |
| Keyboard | Type, keyboard language, and number of keys |
| Monitor | Manufacturer and model, maximum resolution, vertical and horizontal refresh rates |
| Video card | Manufacturer and model number, type of graphics card, the video chipset, amount of video RAM, color depth |
| Sound card | Manufacturer and model, type (Sound Blaster, ESS), IRQ address, I/O port, DMA |
| Printer | Manufacturer and model, type of printer (PostScript, PCL) |

## Task: Printing System Information Using Microsoft Windows

Many computer systems are sold with Microsoft Windows installed. If this is the case for you, you can make the task of collecting system information easier with the aid of the System Properties list. You can view the list of system devices and make a note of them one by one, or you can print the list. To use the Windows operating system to collect system information, follow these steps:

- 1. Open the System Properties dialog box. There are several ways to access this dialog box. Right-click the My Computer icon and select Properties from the menu that appears. Or, click Start, Settings, Control Panel, and then double-click the System icon.
- 2. Click the Device Manager tab (shown in Figure 1.1) to display the types of devices installed on the computer.

### FIGURE 1.1
View device information and system resource conflicts from the Windows System Properties dialog box.

![](img/782ecfdc0b083a767896cc983e10427f_38_0.png)

Select a device

Click to view device information

- 3. Click the plus sign next to a device type to expand the list. For each device type, all the devices of that type will appear.
- 4. Click the Print button to display the Print dialog box shown in Figure 1.2.

### FIGURE 1.2
Print the contents of the system properties file.

![](img/782ecfdc0b083a767896cc983e10427f_39_0.png)

Print the complete list

- 5. Select the All devices and system summary option button. This prints a summary of the entire system, including IRQ and I/O port summaries, memory and DMA usage, and disk drive information.
- 6. Click OK to send the report to the printer.

The preceding steps showed you how to print system information. If you'd rather save this information to an electronic text file, follow these steps:

- 1. Open the Microsoft System Information utility. Click Start, Programs, Accessories, System Tools, System Information to display the system information similar to the one shown in Figure 1.3.

### FIGURE 1.3
Microsoft System Information is another way to find hardware information.

Select a category

Display information

![](img/782ecfdc0b083a767896cc983e10427f_39_1.png)

- 2. Display system information. Click the plus sign next to a category and then click the type of information you want to know about the computer.
- 3. Save the system information to a text file. Select File, Export to display the Save As dialog box. Select a directory in which to save the file, give the file a name (such as sysinfo.txt), and click Save.

- 4. View the system information file. Open a text editor, such as Microsoft WordPad, and open the file you created in step 4. A sample report is shown in Figure 1.4.

### FIGURE 1.4
Save system information to a text file for future reference.

![](img/782ecfdc0b083a767896cc983e10427f_40_0.png)

## Getting Ready for the Installation

Since the beginning of Linux, each distribution and each version of each distribution has strived to simplify the installation process. In the early years, the long and tedious installation process kept many people from getting a look at this operating system. Even though the installation process has become more automated and intuitive, you still need to determine your computer's configuration, decide which is the best way to load Linux on the system, and understand the installation process for the Linux distribution you selected.

Before you start the Linux installation, make sure that you are prepared. You'll need to have the following items ready:

- The first thing you'll need is the installation CD-ROM for the Linux distribution you chose. Look at the contents of the CD-ROM for any README files. These files will give you hints as to where you'll find more information on the CD-ROM.
- Collect all the necessary hardware information and read the Linux Hardware Compatibility HOWTO.
- If the computer does not boot from the CD-ROM drive, you will need to create an installation boot disk. It's also a good idea to create this boot disk even if the CD-ROM boots. You might need this disk in an emergency.
