
tus window appears, which shows the name of the file within the x directory (**xmenu2.bmp**) being copied.

![](img/75f39fc91296b889c0653851accdfd46_1232_0.png)

There are a variety of options you can select when running FTP. Notice in Figure 16-17 that the "Transfer Type:" is binary. This is one of the options I selected prior to initiating the transfer.

Although this functionality is not as extensive as the file sharing of NFS, it is widely used to copy files from system to system and therefore can play a role in Windows and UNIX interoperability.

I used icons to specify the information to be copied in this example. You could also have used the FTP command. The following is an overview of FTP, including an example of running it from the command line and a command summary.

| File Transfer Protocol (FTP) | Transfer a file, or multiple files, from one system to another, such as Windows to UNIX. The following example shows copying the file /tmp/krsort.c from system2 (remote host) to the local directory on system1 (local host). |
| :--- | :--- |

```
$ ftp system2
Connected to system2.
system2 FTP server (Version 16.2) ready.
Name (system2:root): root
Password required for root.
Password:
User root logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd /tmp
CWD command successful
ftp> get krsort.c
PORT command successful
Opening BINARY mode data connection for krsort.c
Transfer complete.
2896 bytes received in 0.08 seconds
```

-   comments
    -   Issue ftp command
    -   Log in to system2
    -   Enter password
    -   cd to /tmp on system2
    -   Get krsort.c file
    -   ftp> bye | Exit ftp
    -   Goodbye.
    -   $

In this example, both systems are running UNIX; however, the commands you issue through **FTP** are operating-system-independent. The `cd` for change directory and `get` commands used above work for any operating system on which **FTP** is running. If you become familiar with just a few **FTP** commands, you may find that transferring information in a heterogeneous networking environment is not difficult.

Because **FTP** is so widely used, I describe some of the more commonly used **FTP** commands.

**ftp** - File Transfer Protocol for copying files across a network.

The following list includes some commonly used `ftp` commands. This list is not complete.

-   `ascii` Set the type of file transferred to ASCII. This means that you will be transferring an ASCII file from one system to another. This is the default, so you don't have to set it.
    -   Example: `ascii`

-   `binary` Set the type of file transferred to binary. This means that you'll be transferring a binary file from one system to another. If, for instance, you want to have a directory on your UNIX system that will hold applications that you will copy to non-UNIX systems, then you will want to use binary transfer.
    -   Example: **binary**

-   `cd` Change to the specified directory on the remote host.
    -   Example: **cd /tmp**

-   `dir` List the contents of a directory on the remote system to the screen or to a file on the local system if you specify a local file name.

-   `get` Copy the specified remote file to the specified local file. If you don't specify a local file name, then the remote file name is used.

-   `lcd` Change to the specified directory on the local host.
    -   Example: **lcd /tmp**

-   `ls` List the contents of a directory on the remote system to the screen or to a file on the local system if you specify a local file name.

-   `mget` Copy multiple files from the remote host to the local host.
    -   Example: **mget *.c**

-   `put` Copy the specified local file to the specified remote file. If you don't specify a remote file name, then the local file name is used.
    -   Example: put test.c

-   `mput` Copy multiple files from the local host to the remote host.
    -   Example: mput *.c

-   `system` Show the type of operating system running on the remote host.
    -   Example: **system**

-   `bye/quit` Close the connection to the remote host.
    -   Example: **bye**

**FTP** commands exist in addition to those I have covered here.

# Other Connection Topics

There are other means by which you can connect to the UNIX system. Two popular techniques for connecting to other systems are FTP, which was just covered, and TELNET. NFS Maestro supplies the capability for both of these. I could sit at the Windows system using TELNET with a window open on the UNIX system and issue commands.

Figure 16-18 shows the *HostExplorer* window used to specify the characteristics of your TELNET session.

![](img/75f39fc91296b889c0653851accdfd46_1237_0.png)

I selected VT in the HostExplorer window and was able to log in to the UNIX system, as shown in Figure 16-19.

![](img/75f39fc91296b889c0653851accdfd46_1238_0.png)

Figure 16-19 telnet Window

In this window, we can issue UNIX commands just as if we were sitting at a terminal connected directly to the UNIX system. This window shows /home/hp, including the nfs directory copied earlier, and permissions, owner, and group of all files and directories.

telnet is widely used in heterogeneous environments. With X Windows, you get graphical functionality that is not part of telnet.

The protocols running on the UNIX system are assigned to ports. We can view these ports, protocols, and associated information, using the rpcinfo command on the UNIX system, as shown in Figure 16-20.

![](img/75f39fc91296b889c0653851accdfd46_1239_0.png)

Figure 16-20 rpcinfo Command on UNIX

There is a lot of information in this window in which we are interested related to NFS. We do not, however, have to establish a telnet sessionwith the UNIX system and issue rpcinfo to see this information. The Rpcinfo menu pick under Maestro will query the UNIX host and list the services it is running. Figure 16-21 shows this window.

![](img/75f39fc91296b889c0653851accdfd46_1240_0.png)

*Figure 16-21* *Rpcinfo* Window on Windows

RPC stands for Remote Procedure Call. There are a variety of programs for which there is RPC-related information. Several programs are required to achieve the Windows and UNIX interoperability.

The first number shown is the program number. There are widely accepted RPC numbers for various programs. For NFS, the program number is 10003. The next number is the version of the protocol. In this case, NFS is version 2. The next number is the port. The port number is used by both the client, which is the Windows system in our case, and the server, which is the UNIX system in our case, to communicate using NFS. The next field is the protocol used, which is usually UDP or TCP. The final field is the program name.

In the case of NFS, I had to ensure that NFS, portmapper, mountd, and pcnfds were running on my UNIX system before I could use the NFS Maestro NFS product.

*Rpcinfo* is a useful tool for viewing all the information on the host to which your Windows system will connect.

## CHAPTER 17

### Advanced Server for UNIX

#### Windows Functionality on UNIX

To this point, we have been discussing moving UNIX functionality such as X Windows and NFS onto Windows in order to achieve interoperability. Why not do the converse? Having some Windows functionality on UNIX would certainly be helpful in some cases. UNIX resources such as printers and disks could then be shared with several Windows systems on the network.

Advanced Server for UNIX® is an AT&T product that serves as the basis for many products that bring Windows functionality to UNIX. Advanced Server for UNIX Systems is the result of a joint development agreement between AT&T and Microsoft Corporation. It provides Windows functionality that facilitates Windows and UNIX interoperability. With Advanced Server for UNIX, a UNIX system can act as a Primary or Backup Domain Controller, a file server, a print server, or other Windows functional component. Most major UNIX vendors have a product that is based on Advanced Server for UNIX. This chapter will use the HP-UX implementation of Advanced Server for UNIX called Advanced Server/9000. Other implementations of Advanced Server for UNIX are similar, so you can use the
