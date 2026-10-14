
## Finding the Manuals

Most computer systems include some type of printed manual that describes how to set up and use the system. Unfortunately, this documentation is usually filed in some forgotten corner. Although manuals seem to be getting smaller every year, yours probably contains at least a few key specifications for your system. If you can locate your computer's manual, do the following:

- Look in the index under the name of any hardware component that you want to learn more about.
- Check the table of contents for a section named “Specifications” or “Troubleshooting.”
- Review the first few pages of the section on setting up the system. It may contain other details about the hardware.

Most computers come with separate manuals for each component; each of these manuals is provided by a different manufacturer. (Sometimes these manuals are tucked inside a sleeve with a CD-ROM full of software for the device.) Look for separate manuals on the following items:

- Main system (the CPU)
- Monitor
- Mouse
- Video card
- Modem
- CD-ROM drive
- Sound card

If you can't locate the printed manuals, try going online. Visit the Web site for the manufacturer of the component. Search under Products, Technical Support, or a related topic. Locating technical information on a huge Web site can be time consuming, but this information is generally free. A sample Web page showing the specifications for a Toshiba laptop is shown in Figure 8-5.

## Reviewing BIOS Settings

Sometimes you can find information that is not evident in the printed or online documentation by reviewing the BIOS of the computer itself. Different systems use various methods of accessing the BIOS configuration menus, where you can learn about system status and devices. An onscreen message normally explains how to enter the Setup or BIOS information screen when you first boot the computer. Depending on your system, you might be asked to press F2, Del, Esc, or some other key or combination of keys to enter the BIOS menus. Review the system documentation if you don't see a message explaining how to enter the BIOS menus.

![](img/43f64015de86d989e30eff5bb284fb96_370_0.png)

### Figure 8-5 A sample Web-based specifications sheet

The exact steps for exploring the BIOS menus are not given here because each manufacturer uses a different interface for configuring the BIOS. A sample screen for BIOS configuration is shown in Figure 8-6.

![](img/43f64015de86d989e30eff5bb284fb96_370_1.png)

### Figure 8-6 BIOS configuration menus

Keep the following points in mind as you examine the BIOS menus for hardware information:

- Most BIOS configurations include a number of options that are not relevant to installing Linux. These include things such as the time to wait before entering low-power mode and whether to include a power-on password. You can ignore these options and focus on locating information about devices you need to configure in Linux.
- Different levels of information may be provided in different menus. The details you need for a complex Linux configuration are more likely found in the Advanced portion of the BIOS configuration. Most users don’t need to know this information to use a system that is already up and running.
- You can make changes to the settings in the BIOS and save them as you exit the BIOS setup utility. Don’t do this unless you have studied the system documentation and are familiar with the features you are altering. Watch carefully as you exit the BIOS menus to make sure you do not accidentally choose a Save and Exit option unless you intend to. If you make changes, write down the settings that you alter so that you can change them back to their original values if the computer doesn’t function as expected.

You should find the following information as you review your BIOS settings:

- Amount of RAM on the system
- Hard disk interface type and size of each hard disk
- Serial ports available on the system and the IRQ used by each one
- IRQ numbers used by other devices that might conflict with devices such as a sound card or network adapter (You usually can’t see the IRQ used by these devices in the BIOS menus.)
- SCSI card make and model
- USB port information

Without accessing the BIOS, you can use a related method for locating system information: simply watch the screen carefully as the system starts. Many devices—including SCSI cards, video cards, and add-on IDE cards—will print identification messages to the screen as they are initialized at system start time. Some also prompt you to press a key during their initialization process to enter a setup utility specific to that device. You may have to power the system off and on several times to read the messages, but you can often gain much useful information from these small "advertisements" that are printed on screen.

## Studying Microsoft Windows

If your computer is already running a Microsoft Windows operating system, you can take advantage of the device information that Windows has already discovered. Before installing Linux, you can start your computer in Microsoft Windows and write down all the configuration information you might need to use when installing Linux.

On newer versions of Microsoft Windows, such as Windows XP Professional, you can use the System Information utility to explore detailed information about your computer hardware. On the Start menu, choose All Programs, then Accessories, then System Tools, then System Information. In the left side of the window that appears, you can select which type of hardware you want to learn about. Details appear on the right, as shown in Figure 8-7.

![](img/43f64015de86d989e30eff5bb284fb96_372_0.png)

Figure 8-7 The System Information utility in Microsoft Windows XP Professional

Device information is also available on any version of Microsoft Windows via Control Panel. You can open Control Panel by clicking Start, then Control Panel (or Start, then Settings, then Control Panel in some versions of Windows). You can also double-click the My Computer icon on the Desktop, and then click Control Panel (it may be hidden on some systems). The Windows Control Panel (shown in Classic view) is shown in Figure 8-8. The icons on each Microsoft Windows system vary slightly based on the hardware and software that you have installed; so your screen is likely different from the figure.

![](img/43f64015de86d989e30eff5bb284fb96_372_1.png)

Figure 8-8 The Microsoft Windows Control Panel

Different versions of Windows (such as 98, NT, XP, ME, and 2000) arrange information differently in Control Panel. You can explore several of the Control Panel sections by double-clicking icons that appear to have useful information. For example, you might try double-clicking one or more of the following Control Panel icons (not every icon is available on every version of Windows):

- Devices
- Display, via the Settings tab (choose the Display Type or Advanced Settings button)
- Multimedia, via the Devices tab
- Network, via the Adapters tab
- Ports
- Printers
- SCSI Adapters
- System

In the various lists of devices, you might be able to see the manufacturer and model name in some cases. Within some Windows dialog boxes, you can further research your system's hardware by selecting a hardware device and choosing the Properties button at the bottom of the dialog box or by selecting Properties from a right-click context menu.

You can also use Windows to find details about your networking configuration. Because a computer cannot run both Windows and Linux at the same time, you can normally use the same networking information for Linux that you use for Windows.

Within Windows Control Panel, the Network icon opens a dialog box in which network configuration details are displayed. The Identification tab in the Network dialog box includes a Computer name field with a name for your system. This name is associated with Windows networking, but you may want to use this as your host name when you install Linux. Ask your system administrator for advice.

Within some versions of Windows, the Configuration tab of the Network dialog box lists many different Windows networking components. One item is labeled TCP/IP, followed by the name of your networking device (this is usually an Ethernet networking adapter). Figure 8-9 shows the Network dialog box. The TCP/IP item is normally at the end of the list of network components (it does not appear in the figure).
