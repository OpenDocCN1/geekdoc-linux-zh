# Creating the Print Manager

NDPS-enabled printers have printer agent software embedded in the physical printer, but non-NDPS printers don't, so their printer agent software must run on a NetWare server. Print Manager consists of software and an iDirectory object used to create, manage, and run printer agents for printers without embedded printer agents. The iDirectory object contains configuration information that tells Print Manager software where to store print jobs and which users have rights to perform management tasks. After the Print Manager object is created, Print Manager software needs to be loaded on the server to create and run printer agents. Print Manager also enables administrators to manage and configure printer agents from the NetWare server console. Figure 8-18 shows the relationship between Print Manager, printer agents, and physical printers.

![](bbox=[0.08, 0.24, 0.6, 0.55])

Only one Print Manager at a time can be loaded on a NetWare server.

There's no limit on the number of printer agents that can be controlled from one Print Manager, but a large network can have multiple Print Managers running on separate NetWare servers to delegate administrative tasks or reduce network traffic across routers and WANs, as shown in Figure 8-19.

When printers don't have embedded printer agent software, you need to create and load a Print Manager object in the iDirectory tree before creating printer agents. For the UAS network, the UAS_NDPSM object contains configuration and security information needed to load Print Manager software. When configuring this object, Eric selected the OORP rather than the SYS volume as the location for the print job database. Using a volume other than SYS for storing print jobs protects the SYS volume from filling up with print jobs waiting to be printed. If the SYS volume becomes full, the NetWare server will go down, with the possible loss of data and productivity.

Because of Novell's OneNet strategy, NDPS printer management tasks have been included in iManager rather than in ConsoleOne. NetWare Administrators will notice NDPS management functions from earlier NetWare versions. Although NetWare Administration on iManager can be used to create NDPS objects, Eric elected to use iManager to get more experience with Novell's OneNet strategy. After creating the Print Manager object,