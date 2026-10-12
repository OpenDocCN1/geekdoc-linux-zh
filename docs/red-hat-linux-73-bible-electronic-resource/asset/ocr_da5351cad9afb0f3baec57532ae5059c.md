# ## Chapter 17

# ## Setting up a Print Server

In This Chapter

+   Printing in Red Hat Linux with LPNg
+   Printing in Red Hat Linux with CUPS
+   Choosing a printer
+   Managing document printing in Red Hat Linux
+   Configuring print servers

Sharing printers is a good way to save money and make your printing more efficient. Very few people need to print all the time, but when they do need something printed, they usually need it quickly. Setting up a print server can save money by eliminating the need for a printer at every workstation. Some of those savings can be used to buy special printer features, such as high-speed printing or color.

You can attach printers to your Red Hat Linux system to make them available to users of that system or to other computers on the network. You can configure your Red Hat Linux printer as a remote Linux printer, a Samba printer, or a NetWare printer. With Samba and NetWare, you are emulating those types of servers.

Red Hat Linux can also act as a client, taking advantage of printers on the network. As a client, Red Hat Linux can access local printers, other Linux or UNIX printers, NetWare printers, and printers on Windows or OS/2 systems (using the SMB protocol).

This chapter describes configuring and using printers in Red Hat Linux. It focuses on the LPNg printing service, but it also discusses the merits of replacing LPNg with the Common UNIX Printing Service (CUPS), which is also delivered with Red Hat Linux. The discussion includes configuring printers to emulate printing services for NetWare and Server Message Block (SMB), as well as configuring local printers. For printing documents, Red Hat Linux offers both command-line and GUI tools for configuring printers, as well as several commands for processing text in different formats (such as the troff and TeX commands, which are described in Chapter 6).

Because Red Hat Linux can act as both a print server and a print client, this chapter contains procedures for both types of configurations. The print client is the computer that is sending