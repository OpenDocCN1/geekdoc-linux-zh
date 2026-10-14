
are URLs to each updated package and diskette image in the Errata. By using these URLs, you can then download any necessary diskette images. Remember to use binary mode when transferring a diskette image!

For now, concentrate only on the Errata entries that include new diskette images (the file names always end in .img). If you find an entry that seems to apply to your problem, get a copy of the diskette images, and create them using the instructions in Appendix A.

## Things You Should Know

In order to prevent any surprises during the installation, you should collect some information before attempting to install Red Hat Linux. You can find most of this information in the documentation that came with your system, or from the system's vendor or manufacturer. Please Note: The most recent list of hardware supported by Red Hat Linux can be found at Red Hat Software's World Wide Web site at http://www.redhat.com/hardware. It's a good idea to check your hardware against this list before proceeding.

## Basic Hardware Configuration

You should have a basic understanding of the hardware installed in your computer, including:

- **hard drive(s)** — Specifically, the number, size, and type. If you have more than one, it's helpful to know which one is first, second, and so on. It is also good to know if your drives are IDE or SCSI. If you have IDE drives, you should check your computer's BIOS to see if you are accessing them in LBA mode. Please refer to your computer's documentation for the proper key sequence to access the BIOS. Note that your computer's BIOS may refer to LBA mode by other names, such as "large disk mode". Again, your computer's documentation should be consulted for clarification.

- **memory** — The amount of RAM installed in your computer.

- **CD-ROM** — Most importantly, the unit's interface type (IDE, SCSI, or other interface) and, for non-IDE, non-SCSI CD-ROMs, the make and model number. IDE CD-ROMs (also known as ATAPI) are the most common type in recently manufactured, PC-compatible computers.

- **SCSI adapter (if one is present)** — The adapter's make and model number.
- **network card (if one is present)** — The card's make and model number.
- **mouse** — The mouse's type (serial, PS/2, or bus mouse), protocol (Microsoft, Logitech, MouseMan, etc.), and number of buttons; also, for serial mice, the serial port it is connected to.

On many newer systems, the installation program is able to automatically identify most hardware. However, it's a good idea to collect this information anyway, just to be sure.

## Learning About Your Hardware With Windows®

If your computer is already running Windows 9x, you can use the following procedure to get additional configuration information:

- With Windows running, click on the "My Computer" icon using the secondary (normally the right) mouse button. A pop-up menu should appear.
- Select "Properties." The "System Properties" window should appear (see Figure 2-1). Note the information listed under "Computer." — in particular the amount of RAM listed.

![](img/46f4935125ba89e12897afbe9d77a097_37_0.png)

### Figure 2-1: Windows System Properties Window

- Click on the "Device Manager" tab. You will then see a graphical representation of your computer's hardware configuration. Make sure the "View devices by type" button is selected.

At this point, you can either double-click on the icons (or single-click on the plus sign [+] ) to look at each entry in more detail (see Figure 2-2). Look under the following icons for more information:

![](img/46f4935125ba89e12897afbe9d77a097_38_0.png)

### Figure 2-2: Device Manager Under Windows 95

- Disk drives — You will find the type (IDE or SCSI) of hard drive here. (IDE drives will normally include the word "IDE," while SCSI drives won’t.)
- Hard disk controllers — You can get more information about your hard drive controller here.
- CDROM — Here is where you’ll find out about any CD-ROM drives connected to your computer. Please Note: In some cases, there may be no CD-ROM icon, yet your computer has a functioning CD-ROM drive. This is normal, depending on how Windows was originally installed. In this case, you may be able to learn additional information by looking at the CD-ROM driver loaded in your computer’s config.sys file.
- Mouse — The type of mouse present on your computer can be found here.
