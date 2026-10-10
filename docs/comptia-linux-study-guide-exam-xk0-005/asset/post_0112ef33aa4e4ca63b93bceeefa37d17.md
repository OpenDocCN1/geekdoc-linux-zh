
## Working with PCI Devices

The `lspci` command displays information about PCI devices. The following options are available:

- `-n`: Displays vendor and device information as numbers instead of text
- `-q`: Queries the centralized PCI database for information about the installed PCI cards
- `-t`: Displays a tree diagram that shows the connections between cards and buses
- `-v`: Displays additional information (verbose) about the cards
- `-x`: Displays a hexadecimal output dump of the card information

The output from the `lspci` command without any options shows all devices connected to the system, as shown in Listing 23.8.

### Listing 23.8: Using the `lspci` command

```text
$ lspci
00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02)
00:01.0 ISA bridge: Intel Corporation 82371SB PIIX3 ISA [Natoma/Triton II]
00:01.1 IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)
00:02.0 VGA compatible controller: InnoTek Systemberatung Gmbh VirtualBox
   Graphics Adapter
00:03.0 Ethernet controller: Intel Corporation 82540EM Gigabit Ethernet
   Controller (rev 02)
00:04.0 System peripheral: InnoTek Systemberatung Gmbh VirtualBox Guest
   Service
00:05.0 Multimedia audio controller: Intel Corporation 82801AA AC'97 Audio
   Controller (rev 01)
00:06.0 USB controller: Apple Inc. KeyLargo/Intrinsic USB
00:07.0 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 08)
00:08.0 SATA controller: Intel Corporation 82801IHR/IHEM (ICH9M/ICH9M-E) SATA
   Controller [AHCI mode] (rev 02)
$
```

You can use the output from the `lspci` command to troubleshoot PCI card issues, such as if a card isn't recognized by the Linux system.

## Working with USB Devices

You can view the basic information about USB devices connected to your Linux system by using the `lsusb` command. Table 23.2 shows the options that are available with that command.

### Table 23.2: The `lsusb` command options

| Option | Description |
| :----- | :---------- |
| `-d` | Displays only devices from the specified vendor ID |
| `-D` | Displays information only from devices with the specified device file |
| `-s` | Displays information only from devices using the specified bus |
| `-t` | Displays information in a tree format, showing related devices |
| `-v` | Displays additional information about the devices (verbose mode) |
| `-V` | Displays the version of the `lsusb` program |

The basic `lsusb` program output is shown in Listing 23.9.

### Listing 23.9: The `lsusb` output

```text
$ lsusb
Bus 001 Device 003: ID abcd:1234 Unknown
Bus 001 Device 002: ID 80ee:0021 VirtualBox USB Tablet
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
$
```

Most systems incorporate a standard USB hub for connecting multiple USB devices to the USB controller. Fortunately, there are only a handful of USB hubs on the market, so all Linux distributions include the device drivers necessary to communicate with each of these USB hubs. That guarantees that your Linux system will at least detect when a USB device is connected.

## Supporting Monitors

Two basic elements control the video environment on your Linux system: the video card and the monitor. To display any type of text or graphics, your Linux system must know how to interact with both of them. This is where the X Window System software comes in.

The *X Window System* was developed at the Massachusetts Institute of Technology (MIT) to provide a standard protocol for interacting with displays. The X Window System is most commonly referred to as just X, or X11, since the last version defined is version 11.

The X11 system operates beneath the graphical desktop environment on your Linux system, as shown in Figure 23.1.

### Figure 23.1: The standard Linux graphics environment

![](img/c0a399aca0d18f8822d714ad0a173123_722_0.png)

The job of X11 is to interact with the hardware level of your system's video environment—the video card, monitor, keyboard, and mouse—and provide a standard interface that any desktop management software (such as KDE or GNOME) can use. Because of this, the X11 software must be able to interact with all of those hardware devices.

The original X11 software for Linux was the XFree86 package. This was notorious for being difficult to configure and get working with different types of video hardware. Because of that, newer X11 packages have surfaced and have become more common:

- **X.org**: A user-friendly X11 software package for Linux, developed as a direct replacement for XFree86, but using simple text-based configuration files. It stores configuration files in a common /etc/X11 directory.
- **Wayland**: A simpler, more secure graphical software package, developed by Red Hat, and released as open source software. Wayland is becoming more popular with Linux distributions, quickly replacing even X.org. It stores separate configuration files for each user in the ~/.config/wayland-\*.conf file in each user's home directory.

Both the X.org and Wayland systems attempt to automatically detect the video card, monitor, keyboard, and mouse installed on the system at each boot time and dynamically change the configuration files accordingly. If you make any changes to the video card or monitor, they will automatically detect the new equipment and alter the configuration accordingly, making it a breeze to swap out new video equipment.

**WARNING**  
The X.org and Wayland packages include several different drivers that support common video cards and monitors. For both packages, however, if they don't recognize the specific video card or monitor on your system, they default to using generic drivers that may not produce the best-quality video experience. If your Linux system uses a specialty graphics card or monitor, it's best to obtain the Linux drivers for them and follow the documentation to manually install the updated drivers.

## Using Printers

Just as with the video environment in Linux, printing in Linux can be somewhat complex. With different types of printers available, trying to install the correct printer drivers as well as using the correct printer protocol to communicate with them can be a nightmare.

Fortunately, the *Common Unix Printing System* (*CUPS*) solves many of those problems for us. CUPS provides a common interface for working with any type of printer on your Linux system. It accepts print jobs using the PostScript document format and sends them to printers using a *print queue* system.

The print queue is a holding area for files sent to be printed. The print queue is normally configured to support not only a specific printer but also a specific printing format, such as landscape or portrait mode, single-sided or double-sided printing, or even color or black-and-white printing. There can be multiple print queues assigned to a single printer or multiple printers that can accept jobs assigned to a single print queue.

The CUPS software uses the Ghostscript program to convert the PostScript document into a format understood by the different printers. The Ghostscript program requires different drivers for the different printer types to know how to convert the document to make it printable on a certain type of printer. This is done using configuration files and drivers. Fortunately, CUPS installs many different drivers for common printers on the market and automatically sets the configuration requirements to use them. The configuration files are stored in the `/etc/cups` directory.

To define a new printer on your Linux system you can use the CUPS web interface. Open your browser and navigate to the URL `http://localhost:631`. Figure 23.2 shows the web interface used by CUPS.

![](img/c0a399aca0d18f8822d714ad0a173123_723_0.png)

The CUPS web interface allows you to define new printers, modify existing printers, and check on the status of print jobs sent to each printer. Not only does CUPS recognize directly connected printers, but you can also configure network printers using several standard network printing protocols, such as the Internet Printing Protocol (IPP) or the Microsoft Server Message Block (SMB) protocol.

Aside from the CUPS web interface, there are a few command-line tools you can use for interacting with the print queues:

- `lpc`: Start, stop, or pause the print queue.
- `lpq`: Display the print queue status, along with any print jobs waiting in the queue.
- `lpr`: Submit a new print job to a print queue.
- `lprm`: Remove a specific print job from the print queue.

If you're working from the command line, you can check the status of any print queue as well as submit print jobs. For each of the commands, to specify the printer use the -P command-line option along with the printer name, as shown in Listing 23.10.

### Listing 23.10: Printing from the command line in Linux

```text
$ lpq -P EPSON_ET_3750_Series
EPSON_ET_3750_Series is ready
no entries

$ lpr -P EPSON_ET_3750_Series test.txt
$ lpq -P EPSON_ET_3750_Series
EPSON_ET_3750_Series is ready and printing
Rank  Owner Job  File(s)          Total Size
active rich  1    test.txt         1024 bytes
$
```

The first line in Listing 23.10 uses the lpq command to check the status of the print queue, which shows that the printer is ready to accept new jobs and doesn't currently have any jobs in the print queue. The lpr command submits a new print job to print a file. After the new print job is submitted, the lpq command shows that the printer is currently printing and shows the print job that's being printed.

> Red Hat-based systems use the Automatic Bug Reporting Tool (abrt) to create a report if any kernel-level hardware errors are detected. Red Hat Linux customers can send the report to tech support to help troubleshoot the hardware issue.

## Using Hot-Pluggable Devices

Computer hardware is generally categorized into two types:

- Cold-pluggable devices
- Hot-pluggable devices
