# Printers

Printers come in a wide variety of makes, models, and capabilities. To format and print information, the application running on the client computer must be configured with the correct printer driver for the printer's make and model. Because of the variety of makes and models available, you should have this driver information for configuring network printers so that you can make sure formatted output goes to the correct printer. For example, a client computer might be configured to support both a Lexmark Optra Plus laser printer and a Hewlett-Packard (HP) Deskjet inkjet printer. When a user selects the Lexmark laser printer and prints a document, the network printing configuration must be set up to ensure that the output is sent to the laser printer for which it was formatted.

As shown in Figure 8-5, in queue-based printing, printers can be attached to the network in one of the following ways:

+   - Locally to the print server
+   - Remotely through Novell Client
+   - Directly to the network cable

![](bbox=[0.1, 0.35, 0.95, 0.66])

When configuring the network printing environment, consider the advantages of each attachment method to determine how it affects the way printers are distributed on the network. Many network administrators use a combination of printer attachments, based on the type of printer and its use.

Remotely attached printers are attached to other clients on the network and are also called manual load printers because you must load software manually on the client computer to connect the printer to the print server. After the software has been loaded, print jobs can be sent to the remote printer by using the network cable to transmit packets of printed data from the print server to the client with the remotely attached printer. NetWare includes the NPWIN95 utility, which can be loaded on a Windows 95/98 client computer that has an attached printer. NPWIN95 receives packets of printer output directed to it from the print server, and then prints the output on the attached printer without interfering with the Windows 95/98 client being used for other processing.

The advantage of using remote or manual load printers attached to client computers is that you can select a convenient location for the printer, making it easier for users to retrieve printed output. The disadvantages of these printers include the lack of support for attaching remote printers to Windows 2000 and XP computers,