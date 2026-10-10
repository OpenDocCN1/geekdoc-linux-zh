In addition to the special modules for controlling disk drivers and NICs, NetWare comes with a number of general-purpose NLMs in the SYS:System directory that can be used for a wide range of capabilities, as shown in Table 2-4. In the following sections, you learn about several of these modules that CNAs must be able to use to manage their network file servers.

Table 2-4  General-purpose NLMs
| NLM | Description |
| :--- | :--- |
| CDROM.NLM | Used to mount a CD when it's first inserted in the server's CD-ROM drive. After this module is loaded, it automatically detects the removal and insertion of CDs. |
| DSREPAIR | Checks eDirectory tree replicas for any problems and synchronizes all replicas with the master. |
| NWCONFIG.NLM | Used to work with NetWare partitions, volumes, and system files. |
| MONITOR.NLM | Used to monitor file server performance, hardware status, and memory usage. |
| REMOTE.NLM | Used to view and operate the NetWare server console from a remote computer. Requires a password. |
| RSPX.NLM | Allows the REMOTE module to send and receive console screens and commands over the local network cable. |
| RS232.NLM | Allows the REMOTE module to send and receive console screens and commands over the asynchronous port. |
| RCONAG6.NLM | Provides an IP-based remote Java console for use with ConsoleOne, as described in Chapter 5. |
| SCRSAYER | Provides a method to lock the server console by using a password. To access the server console, the operator must enter the specified password or the Admin user's password. |
| VREPAIR.NLM | Checks the specified traditional volume for errors and allows you to write corrections to the disk volume. This command works only with traditional volumes. To correct problems with NSS volumes, you need to use the NSS /REBUILD command. |

The NLMs shown in Table 2-4 can be classified into three general categories based on their function.

# The Disk Repair Modules

The DSREPAIR and VREPAIR NLMs are used to identify and fix problems in the file system. A major difference between these NLMs is that DSREPAIR is used to work with NSS volumes and VREPAIR is used with traditional volumes. You learn more about NSS and traditional volumes in Chapter 3.

# The Remote Access Modules

NetWare 6.5 has a number of NLMs that support remote access to the server console. The REMOTE, RSPX, and RS232 NLMs are used for backward compatibility with the older Remote console utility, but with NetWare 6.5, you should use RCONAG6.NLM or Remote Manager to access the server console remotely. Remote Manager is Novell's OneNet utility for managing your server environment from a Web browser running on any network. You learn how to use Remote Manager to view your server's performance in “Monitoring the Server with Remote Manager” later in this chapter.

# Server Console Management Modules

The server console management modules include CDROM, MONITOR, NWCONFIG, and SCRSAYER. CDROM mounts a CD onto the file system. MONITOR provides a way of managing your server's performance and is covered in detail in the following section. NWCONFIG provides a number of server configuration options, including modifying the server startup files (see “Modifying Server Startup Files” later