# How do I add a TCP/IP printer to Windows NT?

Click on the Printers options of the Control Panel and then double-click on Add Printer Icon to open the Add Printer Wizard. Select My Computer and then click Next to get to the port selector as shown in Figure 11-5.

Select the Add Port button to add an LPR port, then highlight the LPR Port option, as shown in Figure 11-6, to connect to either a native TCP/IP printer or a UNIX printer with remote printing enabled. Then click New Port.

In the resulting dialog box, type in the name or IP address of the print server or UNIX machine that controls the printer, and then the name of the printer or print queue. If it’s an H-P JetDirect printer, you’ll use RAW as the printer name as shown in Figure 11-7.

Follow the rest of the prompts to complete the process, telling Windows NT what type of printer is being printed to and other details. Don’t forget to print a test page, just in case.

# How can I let my UNIX users use my Windows NT printers?

Unfortunately, Windows NT doesn’t include an lpd (lp daemon), which means it can’t act as a remote printer for

![](bbox=[0.22, 0.74, 0.8, 0.935])

Figure 11-5 You’ll need to add a new port to connect to a TCP/IP printer