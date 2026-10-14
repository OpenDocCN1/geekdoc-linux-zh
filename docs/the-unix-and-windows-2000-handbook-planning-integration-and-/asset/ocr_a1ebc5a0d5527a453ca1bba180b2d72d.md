Source for the LPRng distribution can be obtained at `http://www.astart.com/lprng/`. The distribution contains a script that determines your type of system and sets options for compilation and installation. The distribution also contains detailed instructions on disabling the default print services for your version of UNIX. LPRng is a great choice for heterogeneous networks.

# COMMON UNIX PRINTING SYSTEM

The Common UNIX Printing System (CUPS) is a portable printing layer for UNIX operating systems. It provides SysV and BSD command-line interfaces. The Internet Printing Protocol (IETF-IPP) is utilized as the basis for managing printers and queues. It also provides support for BSD and SMB protocols. The distribution can be obtained at `http://www.cups.org/`. Binary distributions for HPUX, Solaris, and Linux are available, in addition to the source code.

# Windows 2000 Print Services

Windows 2000 makes for a very good print server, but you must deploy hardware that can handle the load you will place on the server. While you could simply have your users print directly to the printers themselves, it is more efficient to use a print server to process and queue the users’ print requests. This section will discuss how to deploy a capable print server, connect that server to your printers, add the printer driver, and share the printer to your clients. You will also learn how to connect your clients to shared printers, as well as how to provide printing services to UNIX systems.

# PRINT SERVER SYSTEM REQUIREMENTS

Any system you plan to deploy as a print server should meet the minimum requirements for installing Windows 2000 Server. This system must also be capable of processing print jobs effectively given the load you plan to put on the server. The following configuration should be considered a minimum for a print server running Windows 2000 Server:

+   - 256MB RAM.
+   - 9GB storage.
+   - 100 Mb/s network interface.

As your network grows, you may want to consider upgrading your server or deploying additional servers to distribute your printing load.