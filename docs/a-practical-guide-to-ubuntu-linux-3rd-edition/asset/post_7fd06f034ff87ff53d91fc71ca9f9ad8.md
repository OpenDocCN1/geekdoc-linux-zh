
## CUPS 1.4.3

CUPS is the standards-based, open source printing system developed by Apple Inc. for Mac OS X and other UNIX-like operating systems.

### CUPS for Users
- Overview of CUPS
- Command-Line Printing and Options
- What's New in CUPS 1.4
- User Forum

### CUPS for Administrators
- Adding Printers and Classes
- Managing Operation Policies
- Printer Accounting Basics
- Server Security
- Using Kerberos Authentication
- Using Network Printers
- cupsd.conf Reference

### CUPS for Developers
- Introduction to CUPS
- Programming
- CUPS API
- Filter and Backend Programming
- HTTP and IPP APIs
- PPD API
- Raster API
- PPD Compiler Driver Information
- File Reference

![](img/2344fc4a798f29dca9e8b5ed7288171a_606_0.png)

**Figure 14-8** The Welcome page

Display the CUPS Web interface by pointing a Web browser at localhost:631 on the system on which you are configuring the printer (Figure 14-8).

### Add Printer

#### Local Printers:
- Brother HL-2140 series (Brother HL-2140 series)
- SG31 Printer
- HP Printer (HPLIP)
- Serial Port #1
- Serial Port #2
- LPT #1
- HP Fax (HPLIP)

#### Discovered Network Printers:
- HP LaserJet P2015 Series (13A428) (HP HP LaserJet P2015 Series)
- HP LaserJet P2015 Series (13A428) (HP HP LaserJet P2015 Series)
- HP LaserJet P2005d (88C08A) (HP HP LaserJet P2005d)
- HP LaserJet P2005d (88C20A) (HP HP LaserJet P2005d)
- HP LaserJet P2005d (88C208) (HP HP LaserJet P2005d)
- HP LaserJet P2005dn (8E5203) (HP HP LaserJet P2005dn)
- HP LaserJet P2005dn (8E5203) (HP HP LaserJet P2005dn)
- HP LaserJet P2005d (HP LaserJet P2005d)
- TASKalfa 2550c (Kyocera TASKalfa 2550c)
- HP LaserJet P2015 Series (HP LaserJet P2015 Series)
- HP LaserJet P2005d (HP LaserJet P2005d)

#### Other Network Printers:
- Internet Printing Protocol (ipp)

![](img/2344fc4a798f29dca9e8b5ed7288171a_606_1.png)

**Figure 14-9** The first Add Printer page

![](img/2344fc4a798f29dca9e8b5ed7288171a_607_0.png)

Clicking the **Administration** tab near the top of the page displays the Administration page. On this page click **Add Printer** to display the first Add Printer page (Figure 14-9). Click the printer you want to install and then click **Continue** to display the second Add Printer page (Figure 14-10). Enter the name of the printer in the text box labeled **Name**; this name must start with a letter and not contain any SPACES. You must supply a name—any name you like. Optionally, you can fill in the text boxes labeled **Description** and **Location** with text that will help users identify the printer. Put a tick in the check box labeled **Sharing** if you want to share the printer. Click **Continue**.

The next screen asks you to select the model of the printer you want to set up (Figure 14-11, next page). Select the printer you want to use. Click **Add Printer**. If the printer is PostScript capable but is not listed, select a PostScript printer such as the Apple LaserWriter 12/640ps. If the printer is not PostScript capable and is not listed, check whether the printer supports PCL; if it does, select another, similar PCL printer. If all else fails, determine which listed printer is most similar to the one you are configuring and specify that printer. You can also try configuring the printer using **system-config-printer** (page 550), which offers a different choice of models.

After you click **Add Printer**, the CUPS Web interface displays the Set Default Options page. This page allows you to set printer options and configuration information. Click the buttons at the top of the page, browse through the selections, and make any changes you like. Frequently you need change nothing. Click **Set Default Options**.

![](img/2344fc4a798f29dca9e8b5ed7288171a_608_0.png)

**Figure 14-11** The third Add Printer page

After displaying a brief message, the CUPS Web interface displays the Printer page (Figure 14-12) showing the new printer. Click **Maintenance ⇔ Print Test Page** to confirm the new setup works. If you want to make this printer the default printer, click the button labeled **Administration** and select **Set As Server Default**.

The buttons at the bottom of the Printer page enable you to cancel or move jobs in the print queue. In addition to these tasks, you may be able to reprint jobs. Figure 14-12 shows the Printer page displaying information about a job the printer is printing.

## TRADITIONAL UNIX PRINTING

Before the advent of GUIs and WYSIWYG (page 1181) word processors, UNIX users would create documents using an editor such as **vi** and a typesetting markup language such as **TeX** or **nroff/troff**, convert the resulting files to PostScript using an interpreter, and send the PostScript files to the printer using **lpr** (or **lp** (System V)). Ubuntu implements both BSD and System V command-line printing utilities for compatibility. However, these utilities are now wrappers around the equivalent functionality in CUPS rather than core components of the printing system. The corresponding utilities are functionally equivalent; use whichever you prefer (Table 14-2).

The **cups-bpd** package holds the BSD utilities; the **cups-client** package holds the System V utilities. From the command line, you can print a text, PostScript, or PDF file using **lp**:

```
$ lp memo.txt
request id is MainPrinter-25 (1 file(s))
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_609_0.png)

**Figure 14-12** Printer page showing jobs information

| BSD/SysV | Purpose |
| :--- | :--- |
| lpr/lp | Sends job(s) to the printer |
| lpq/lpstat | Displays the status of the print queue |
| lprm/cancel | Removes job(s) from the print queue |

The preceding command adds **memo.txt** to the print queue of the default printer as job 25. When this printer is available, it prints the file. You can specify a printer using the `-d` option:

```
$ lp -d ColorPtr graph.ps
request id is ColorPtr-26 (1 file(s))
```

The lpr `-P` option is equivalent to the lp `-d` option. Without arguments, lp and lpr send their standard input to the printer:

```
$ cat memo2.txt | lp
request id is MainPrinter-27 (1 file(s))
```

The lpq and lpstat commands display information about the print queue:

```
$ lpstat
MainPrinter-25   zach   13312   Sun Feb 21 18:28:38 2010
ColorPtr-26   zach   75776   Sun Feb 21 18:28:48 2010
MainPrinter-27   zach   8192   Sun Feb 21 18:28:57 2010
```

Use cancel or lprm to remove jobs from the print queue. By default, only the owner of a print job or a user working with root privileges can remove a job.

```
$ cancel 27
$ lpstat
MainPrinter-25   zach   13312   Sun Feb 21 18:28:38 2010
ColorPtr-26   zach   75776   Sun Feb 21 18:28:48 2010
```

Give the command `sudo cancel -a` or `sudo lprm -` to remove all jobs from the print queues.

## CONFIGURING PRINTERS

You can use the Web interface or the command-line interface to CUPS to manage printers and queues.

### THE CUPS WEB INTERFACE

To connect to the CUPS Web interface (page 555), point a Web browser running on the local system at localhost:631. You must be a member of the lpadmin group (page 597) to change the printer configuration using the CUPS Web interface.

### MODIFYING A PRINTER

“JumpStart II: Setting Up a Local or Remote Printer Using the CUPS Web Interface” (page 555) discusses how to set up a printer using the CUPS Web interface. This section explains how to modify a printer that is already set up.

To modify a printer, click the Printers tab near the top of the page and then click the name of the printer you want to modify. The CUPS Web interface displays two drop-down lists near the top of the page: Administration and Maintenance (Figure 14-12, page 559). These lists work with the selected printer. The Administration drop-down list allows you to modify the printer; this selection takes you through the same steps as when you set up a new printer. From this list you can also delete and set default options for the printer as well as set the printer as the default printer and specify which users are allowed to use the printer. From the Maintenance drop-down list, you can print a test page and pause the printer. You can also reject, move, and cancel all jobs.

### JOBS

Click the Jobs tab near the top of the page to display the Jobs page, which lists jobs in the print queues. From this page you can cancel print jobs and move them to other queues. Click Show Completed Jobs to display a list of recently completed jobs. In some cases, you can reprint completed jobs from this page. You can perform the same tasks from the Printer page.
