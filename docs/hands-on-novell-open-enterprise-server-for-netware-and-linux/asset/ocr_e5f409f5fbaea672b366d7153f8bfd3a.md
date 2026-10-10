the additional setup time to load NPTWIN95 on Windows 95, 98 computers, the need to leave the client computer on to access network printers, and the possible decrease in printing performance for large graphical print jobs. This performance decrease is caused by applications running on the client computer and the extra load on the network cable when sending printer output from the print queue to the network printer.

**Locally attached printers** are attached directly to a printer port on the NetWare server running the print server. In NetWare, these printers are also referred to as **automatic load printers** because there’s no need to load additional software, as with remote or manual load printers. When using local or automatic load printers, the output is sent directly from the print server to the printer through ports on the NetWare server. Local printers can be attached to the **parallel port (LPTn)** or **serial port (COMn)** of the server running the print management software. Compared to remote or manual load printers, the advantages of local or automatic load printers include better printing performance and reduced network traffic. The improved performance is a result of less software overhead because the print server doesn’t have to communicate with a client computer. Network traffic is reduced because print jobs don’t need to be sent from the print server running on a NetWare server to a printer attached to a client on the network.

**Network attached printers** have their own built-in network card, which allows them to communicate directly with computers on the network. Today, network attached printers are rapidly becoming the most common type of network printer. However, the NetWare queue-based printing system was designed before the age of network attached printers, and the print server software isn’t designed to communicate directly with network attached printers. To use a network attached printer with the NetWare print server, the printer must be configured to appear as a remote or manual load printer. You learn more about using network attached printers in “Using the Open Enterprise iPrint System” later in this chapter.

# Setting Up a Queue-Based Printing System

Setting up a queue-based printing system involves these basic steps:

+   1. Create a print queue for each printer.
+   2. Create an eDirectory printer object to represent each printer.
+   3. Create a print server object to send output from print queues to the corresponding printer.
+   4. Load the print server and any remote print software.

Although Novell still supports the queue-based printing system, it hasn’t included management components for it in ConsoleOne or iManager, so you need to use NetWare Administrator. In the following activities, you use NetWare Administrator to perform these setup steps so that you can create print queues, print servers, and printer objects. To load the print server software (PSERVER.NLM) on a NetWare 6.5 Open Enterprise server, IPX must be installed on the NetWare server (see Chapter 2). In addition, only one iteration of the print server can be loaded at one time.

> NOTE
> 
> If you’re using a shared classroom server, you need to coordinate the final activity of loading and testing your print server with other students in the class.
> If you’re using a dedicated NetWare server, you can perform all these activities on your server. If you don’t have a printer attached, you can still perform the activities and view the output in your print queue.

# Activity 8-1: Creating a Print Queue

**Time Required:** 10 minutes
**Objective:** Set up a queue-based printing system.
**Requirements:** A Windows XP computer with Novell Client installed
**Description:** Before setting up a queue-based printer, you need to define the names of the print queue, printer, and print server and determine in what context to place these objects. After determining this information, Eric Kenton used NetWare Administrator to create queue-based printing objects. In this activity, you use NetWare Administrator to create a print queue object in your iAS tree.