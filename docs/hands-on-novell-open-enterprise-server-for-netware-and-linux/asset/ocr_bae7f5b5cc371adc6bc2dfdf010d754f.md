# INTRODUCTION TO NETWORK PRINTING

As shown in Figure 8–1, the basic function of network printing is to send output formatted by an application running on the user’s computer to a shared printer attached to the network.

![](bbox=[0.07, 0.14, 0.78, 0.51])

Because a printer can print output from only one application at a time, network printing needs to control the flow of output from multiple user applications to a single network printer. In previous versions of NetWare, network printing has been accomplished by sending output from a printer driver on a user’s computer to a print job on a server, where it’s held in a print queue until the network printer it needs is available. Print server software running on the NetWare server then transfers the print job to the physical printer attached to the server’s printer port or attached remotely to a client computer. This network printing system, known as *queue-based printing*, is still supported by NetWare 6.5. To format and print information with this system, the application running on a client computer must be configured with the correct printer driver for the network printer’s make and model. In the queue-based system, you have to select this driver manually and make sure it’s up to date. In the following section, you learn how to set up a queue-based printing system in NetWare Administrator.

# Overview of the NetWare Queue-Based Printing System

Queue-based printing, available since NetWare 3, was designed to support simple printers and DOS-based applications. Because many older NetWare networks still use queue-based printing, as a CNA, you should be familiar with its basic components and operation. Before setting up a queue-based printing environment, you need to understand how its basic components work together. As shown in Figure 8–2, the queue-based system consists of three major components, discussed in more detail in the following sections:

+   • Print queue
+   • Print server
+   • Printer