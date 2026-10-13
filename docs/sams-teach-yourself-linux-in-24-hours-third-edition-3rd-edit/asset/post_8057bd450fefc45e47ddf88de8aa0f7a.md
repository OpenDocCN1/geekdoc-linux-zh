
FIGURE 11.2
The printtool will easily configure printers attached to the system.

![](img/782ecfdc0b083a767896cc983e10427f_204_0.png)

FIGURE 11.3
The printtool automatically sets default print service information.

![](img/782ecfdc0b083a767896cc983e10427f_204_1.png)

5. Make a note of the printer information. The printtool uses default values to set up the print services.

> Color inkjet printers can be expensive to operate. If you want to limit the size of the files that can be sent to the printer, type the maximum file size that will be accepted by the printer in the File Limit in KB text box.

6. Click the Select button. This displays the Configure Filter dialog box shown in Figure 11.4.

7. Select the printer manufacturer and model from the Printer Type list. Change any other options as needed and click OK when you are finished. You will be returned to the Edit Local Printer Entry dialog box.

8. Click OK to return to the printtool main window. The printer should now be listed.

FIGURE 11.4
Choose a printer and set print options.

![](img/782ecfdc0b083a767896cc983e10427f_205_0.png)

9. Test the printer. Select the printer from the list and click Tests. Print ASCII Test Page. The test page is sent to the print spool directory and should print on the printer. If the page did not print correctly, click Edit and change the printer configuration.

10. After you have the text test page set up the way you like, try to print a PostScript test page.

11. When you are finished, click PrintTool, Quit.

## Troubleshooting the Print System

As you set up the printer and the print services, you may run into a few problems. Here are a few ideas to help:

- If the text is stair-stepped on the printed page, select the Fix Stair-Stepping Text option when you select the printer type in printtool.
- If your printer is not on the printer type list, select a printer that it will emulate or a printer that closely matches your printer. You may need to find the printer user manual to dig up this information.
- When printing several pages, the last page may not eject from the printer. Use the Send EOF After Job to Eject Page option.
- Other tools are available that you can use to manage your printer. Try the Linux MetaLab Archives at metalab.unc.edu/pub/Linux/system/printing/INDEX.html. For those with HP LaserJet printers, there's a control panel that allows you to change the printer properties (see Figure 11.5).

FIGURE 11.5

The Ljet Tool makes it easy to print with any HP LaserJet printer.

Change resolution

Change paper size and orientation

![](img/782ecfdc0b083a767896cc983e10427f_206_0.png)

## Task: Sending Files to the Printer

Now that your printer is set up and ready to go, you'll want to start sending files to the printer. It's most likely that you'll be working in a graphical environment and you'll just press a print button in the application in which you are working. If this is the case, the file is just sent to the printer and you don't need to worry about a thing. You can also send a file to the printer by using the lpr command. Here's how to send files to the print spool and how to manage the print spool:

1. Send the file to the printer. To print a file, type `lpr filename` and press Enter. In the example shown in Figure 11.6, the user (the superuser, in this instance) listed the directory contents and then selected two files to print. This command sends the file to the print spool (for the default printer, named lp by default in printtool) where it waits until the printer is available.

View print jobs in the print spool

Send files to printer

FIGURE 11.6

View the list of jobs sent to the printer and remove print jobs if necessary.

![](img/782ecfdc0b083a767896cc983e10427f_206_1.png)

Remove print jobs from the print spool

![](img/782ecfdc0b083a767896cc983e10427f_207_0.png)

Be efficient when issuing commands. Instead of issuing two separate lpr commands to send two files to the printer, use one command and specify all the files. To send multiple files to the printer, type `lpr filename file-name` and press Enter.

2. If a second printer is set up, send a file to that printer. Type `lpr -P printername filename` and press Enter. For example, to send the file named install.log to the printer named lp0, type `lpr -P lp0 install.log`.

3. Check on the status of the files in the print spool. Type `lpq` and press Enter. This command lists all the jobs that are either being processed by the printer or are waiting to be processed, and in the order that the jobs will be processed.

4. Delete a job from the print spool. Type `lprm jobnumber` and press Enter. The jobnumber is the number listed in the Job column of the output of the lpq command. For example, in Figure 11.6, to remove the file named kernel1.txt from the print spool, type `lprm 7` and press Enter.

5. Clear all the print jobs that belong to your user account. Type `lprm -` and press Enter. If you execute this command as the superuser, all the print jobs will be removed from the print spool.

## Summary

In this hour, you learned how to set up print services in Linux so that you can print the files you've created. You saw how Linux doesn't actually send a file to the printer right away. It first puts the file in a spool directory until the line printer daemon knows that the printer is available for use. You learned that each distribution uses the print utility in different ways to configure a printer and print services and that this configuration information is stored in the `/etc/printcap` file. Also, because mistakes do happen, you learned how to delete a print job from the spool directory.

## Q&A

Q What are some of the applications (in addition to Ljet) that I can use to make it easier to work with my printer?

A The Ljet tool makes it easy to work with HP LaserJet printers. Also included with KDE is a print spool monitor called Printer Queue, or k lpq. If you use KDE, you may have noticed the printer icon on the desktop. When you drag a file from the file manager and drop it onto the printer icon, the lpr command is executed. There's also a printer applet you can place on the GNOME panel.

## Q Where can I learn more about the Linux print system?

A Start with the HOWTOs. The Linux Printing HOWTO for Linux shows how to set up a printer, configure printing software, find fax software, and preview files before they are sent to the printer. The Linux Printing Usage HOWTO tells how to print different file formats. If you have a Hewlett Packard printer, you should read the HP HOWTO

## Workshop

Test your knowledge of the material covered in this hour by answering the following questions and working through the exercises.

## Quiz

1. What happens when you tell Linux that you want to print a document?

Pressing the print button in an application executes the lpr command. You can also execute the lpr command from the shell prompt. The lpr command takes the specified file and places it in the print spool directory for the printer that will print the file. The file waits in the spool for the line printer daemon, which spawns itself so that it can process the file and send it to the printer as soon as the printer is available.

2. Which command do you use to find out the device name of the port to which the printer is attached?

Use the dmesg command. You'll probably want to view the output of the command in a pager, such as less, so that you can read the entire contents. The printer device information lists the manufacturer and model of the printer attached to the port and the port name (either lp0, lp1, or lp2).

3. What can you do to make sure there's a connection between the operating system, the device file, and the printer?

Send a small text file to the printer or direct the output of a command (such as the ls command) to the printer device with a command like

```
ls > /dev/lp0
```

4. Where is the printer configuration information stored?

All the printer configuration utilities store printer information in the `/etc/printcap` file. It is not recommended that you manually edit the `/etc/printcap` file because the structure is complex and you don't want to make an incorrect change.
