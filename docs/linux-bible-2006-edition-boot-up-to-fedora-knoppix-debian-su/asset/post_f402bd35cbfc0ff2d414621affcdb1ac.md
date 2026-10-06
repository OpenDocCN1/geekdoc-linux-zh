
# Chapter 26 ✦ Running a Print Server 695

From the computer at address 10.0.0.5, you would type:

```
http://localhost:631/admin
```

(substituting the CUPS server's name or IP address for localhost), and when prompted, enter the username and password.

Now, with the Admin screen displayed, here's how to set up a printer:

- 1. Click the Add New printer screen appears.
- 2. Type a name, location, and description for the printer and click Continue.
- 3. Select the device to which the printer is connected. The printer can be connected locally to a parallel, SCSI, serial, or USB port directly on the computer. Alternatively, you may select a network type for Apple printers (Socket/HP JetDirect), Internet Printing Protocol (http or ipp), or a Windows printer (using SAMBA or SMB).
- 4. If prompted for more information, you may need to further describe the connection to the printer. For example, you may need to enter the baud rate and parity for a serial port, or you might enter the network address for an IPP or Samba printer.
- 5. Select the make of the printer driver (if you don't see the manufacturer of your printer listed, choose PostScript for a PostScript printer or HP for a PCL printer). For the make you choose, you will be able to select a specific model.
- 6. If the printer is added successfully, the next page shows a link to the description of the printer. Click that link. From the new printer page, you can print a test page or modify the printer configuration.

After you are able to print from CUPS, you can return to the CUPS Web-based administration page and do further work with your printers. Here are a few examples of what you can:

- ✦ List printer jobs—Clicks to see what print jobs are currently active from any of the printers configured for this server. Click Show Completed Jobs to see information about jobs that are already printed.
- ✦ Create printer printer—Click Classes; then Add Class and identify a name and location for a printer class. Click Continue. Then, from the list of Printers configured on your server, select the ones to go into this class.
- ✦ View printers—You can click the Printers link from the top of any of the CUPS Web-based administration pages to view the printers you have configured. For each printer that appears, you can click Stop Printer (to stop the printer from printing but still accept print jobs for the queue), Reject Jobs (to not accept any further print jobs for the moment), or Print Test Page (to print a page). Figure 26-2 shows the Printers.

# 696 Part V ♦ Running Servers

![](img/a2d958d7eab32ca5b89b2b8af808aa70_727_0.png)

Figure 26-2: Print tests or temporarily stop from the Printers page.

## Using the Red Hat Printer Configuration Window

If you use Fedora, RHEL, or other Red Hat Linux systems, you can use the Printer Configuration window to set up your printers. In fact, it's recommended that you use it instead of CUPS Web administration because the resulting printer configuration files are tailored to work with Red Hat systems.

To install a printer under GNOME desktop in Fedora, start the Printer Configuration window by selecting Setting: Printing (or as root user by typing `system-config-printer`). This tool lets you add and delete printers and edit printer properties. It also lets you test pages to those printers to make sure they are working properly.

The key here is that you are configuring printers that are managed by your print daemon (cupsd for the CUPS service). After a printer is configured, users on your local system can use it. Subsequently, you can refer to the "Configuring Printer Servers" section to learn how to make the server available to users from other computers on your network.

The printers that you set up can be connected directly to your computer (as a parallel port) or to another computer on the network (for example, from another UNIX system or Windows system).

# Chapter 26 ✦ Running a Printer Server 697

## Configuring Local Printers in Red Hat

Add a local printer (in other words, a printer connected directly to your computer) with the Printer Configuration window using the following procedure. (See the "Choosing a Printer" sidebar if you don't yet have a printer.)

- Connect your printer before starting this procedure. This enables the printer software to autodetect the printer's location and to immediately test the printer after you have finished adding it.

### Choosing a Printer

The PostScript language is the preferred format for Linux and UNIX printing and has been for many years. Every major word-processing product that runs on Fedora, Red Hat, SUSE, Debian, and UNIX systems support PostScript printing, so a printer that natively supports PostScript printing is sure to work in Linux.

If you get a PostScript printer and it is not explicitly shown in the list of supported printers, simply select the PostScript filter when you install the printer locally. No special drivers are needed. Your next step is to choose a printer that supports PCL. In either case, make sure that the PostScript or PCL is implemented in the printer hardware and not in the Windows driver.

Avoid printers that are referred to as Wininters. These printers use nonstandard printing interfaces (other than PostScript or PCL). Support for these low-end printers is hit or miss. For example, some low-end HP DeskJet printers use the pm2ppa driver to print documents pbm217kr to print. Although these drivers are available for many Windows, many of them are not fully supported.

Ghostscript may also support your printer; if it does, you can use it to do your printing. Ghostscript (at www.ghostscript.com) is a free PostScript-interpreter program. Ghostscript can convert PostScript content to output that can be interpreted by a variety of printers. There are both GNU and Aladdin Ghostscript drivers available. The latest Aladdin are not immediately licensed under the GPL, so you can use Aladdin drivers if

You'll find an excellent list of printers supported in Linux at www.linuxprinting.org (select the Printer Listing link). I strongly recommend that you visit that site before you purchase a printer to work with Linux. In addition to showing supported printers, the site also has a page describing how to choose a printer for Linux (www.linuxprinting.org/suggested.html).

## Adding a Local Printer in Red Hat

To add a local printer from Fedora or other Red Hat Linux systems, follow these steps:

- 1. Select System Settings Printing from the main menu or type the following as root user from a Terminal window:
`system-config-printer &`
The Printer Configuration window appears.
- 2. Click New. Add a New Print Queue window appears.
- 3. Click Forward. The Queue name window (Figure 26-3).

![](img/a2d958d7eab32ca5b89b2b8af808aa70_729_0.png)

Figure 26-3: Add printers connected locally or remotely with the Printer Configuration window.

- 4. Add the following information:
    - Add the name you want to give to identify the printer. The name must begin with a letter, but after the initial letter, it can contain a combination of letters, dashes (-), and underscores (_). For example, an HP printer on a computer named maple could be named hp-maple.
    - Add a few words describing the printer, such as its features (an HP LaserJet 2100m with PC and PSL support) or its location (in Room 205 under the coofleet).
- 5. Click Forward. The Queue window appears.
- 6. Select Locally, choose the device to which the printer is connected (/dev/lp10, /dev/usb/lp0, and /dev/tty50 are the first pair, parallel, and serial, respectively), and click Forward. (Type ipinfo -v | less to see all ports). Alternatively, If your printer is not on the list because you have not yet connected it, connect it and select Rescan to have your computer try again to detect the printer.

# Chapter 26 ✦ Running a Printer Server 699

- If you intend to connect later, click Custom Device and specify the device name where the printer will be found.
- 7. Click Forward. The Printer window opens.
- 8. Click the Select Manufacturer box, then choose the manufacturer of your printer. From the list that appears, select your printer model.

If your printer doesn't appear on the list but supports PCL (HP's Printer Control Language), try selecting one of the HP printers (such as LaserJet). If your printer supports PostScript, select PostScript from the list. Selecting Raw Print Queue enables you to send to the printer documents that are formatted for your type.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_730_0.png)

- 9. Click the Notes button. In many cases, you'll see good information from the Linux Printer Database about how your printer is configured and how to tune it. (Close the information window when you are done.) Click OK to continue.
- 10. If the information looks correct, click Finish to create the entry for your printer.
- 11. A pop-up window asks if you want to print a test page. Click Yes, and click again when told the test page has printed interesting information about your printer, the resolution, and the type of interpreter used (such as PostScript), for example.

The printer appears in the main Printer Configuration window. If it is the only printer configured, a check mark appears next to it, identifying it as the default printer. As you add other printers, you can change the default printer by selecting the one you want and clicking the Default button.
- 12. From the Printer Configuration window, choose Apply to save the changes (if necessary). If you have no other printers to add, you can close the Printer Configuration window at this point (Action Quit), or you can try tests.

If you like to test other pages, click Test and select one of the following:

- Letter PostScript test page — Sends a letter-sized (8.5 x 11 inch) page to the printer in PostScript format. If you have a color printer, the page appears in color.
- A4 PostScript test page — Sends an A4 PostScript-formatted page to the printer.
- ASCII test page — Sends plain text to the named printer.
- Duplex test — Sends a test page to see if the printer is in half or full duplex.
- JPEG test — Sends a JPEG image to the printer.
