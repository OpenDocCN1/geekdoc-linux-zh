# CHAPTER 12 Printing Services

Click the Continue button. You can then select the type of printer access (local, remote, serial port, or Internet) in the Device page as shown in Figure 12.17. For example, to configure a remote printer, the LPD/LPR Host or Printer entry is used.

![](bbox=[0.168, 0.175, 0.832, 0.545])

Figure 12.17 Select a type of printer access device.

Again click Continue and enter a device URI as requested in Figure 12.18. URIs describe a number of different printer access mechanisms, such as an HTTP resource locator (URL), local serial- or parallel-port, or remote Internet printers. Our example requires a remote UNIX host lpd1pr printer, such as
nlpd://192.168.2.35/1p, which represents the IP address of the remote printer server and the name of the remote print queue on the server.

After you click Continue, you will then select the Model/Make of the printer and a driver. As shown in Figure 12.19, to print a test page, stop printing service, manage the local print queue, modify the printer entry, or add another printer.

CUPS offers many additional features and once installed, running, provides transparent traditional UNIX printing support on your Red Hat Linux system.

To learn more about CUPS and to get a basic overview of the system, browse to
http://www.cups.org/overview.html.