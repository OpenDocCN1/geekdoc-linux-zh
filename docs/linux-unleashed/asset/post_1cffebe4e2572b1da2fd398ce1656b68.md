
have the regular ASCII characters), the mode of the transfer had to be manually changed from ASCII (often called text) to binary. FTP enables file transfers in several formats, which are usually system-dependent. The majority of systems (including UNIX systems) have only two modes: text and binary. Some mainframe installations add support for EBCDIC, while many sites have a local type that is designed for fast transfers between local network machines. (The local type may use 32- or 64-bit words.)

To change the format of the file transfers to allow you to move any file other than a text file, you must first make sure FTP is in binary mode with this command:

```
bin
```

You can return to character mode with the command

```
ascii
```

It's important to be aware of which mode you are in. Linux FTP, by default, usually starts in character (ASCII) mode.

Text transfers use ASCII characters separated by carriage-return and newline characters, whereas binary enables transfer of characters with no conversion or formatting. Binary mode is faster than text and also enables for the transfer of all ASCII values (necessary for non-text files). On most systems FTP starts in text mode, although many system administrators now set FTP to binary mode for their users' convenience. FTP cannot transfer file permissions, as these are not specified as part of the protocol. Some FTP clients and servers can detect the type of file and adjust themselves accordingly. If in doubt, use binary.

Usually there are no keyboard shortcuts (such as pressing the Tab key to fill in names that match) available with FTP. This means you have to type in the name of files or directories in their entirety (and correctly). If you misspell a file or directory name, you will get error messages and have to try again. Luckily, if you are performing the FTP session through an X Window or Windows environment, you can cut and paste lines from earlier in your session.

## Anonymous FTP Access

FTP requires a user ID and password to enable file transfer capabilities, but there is a more liberal method of allowing general access to a file or directory called *anonymous FTP*. Anonymous FTP removes the requirement for a login account on the remote machine, usually allowing the login anonymous with a password of either *guest* or the user's actual login name. The following session shows the use of an anonymous FTP system:

```
ftp> ftp uofc.edu.  
Connected to uofc.edu.
220 uofc.edu FTP server ready.
Name (uofc:username): anonymous
331 Guest login ok, send userID as password.
Password: tparker
230 Guest login ok, access restrictions apply.
ftp>
```

If the remote system is set to allow anonymous logins, you will sometimes be prompted for a password and then given a warning about access limitations. If there is a file on the remote system you require, a get command will transfer it. Anonymous FTP sites are becoming common, especially with the expanding interest in the Internet.

If anonymous FTP is supported on a remote system, a message usually tells you exactly that. The login shown below is for the Linux FTP archive site called sunsite.unc.edu:

```
ftp sunsite.unc.edu
331 Guest login ok, send your complete e-mail address as password.
Enter username (default: anonymous)
Enter password [tparker@tpci.com]:
|FTP| Open
230-  WELCOME to UNC and SUN's anonymous ftp server
230-  University of North Carolina
230-  Office FOR Information Technology
230-  SunSITE.unc.edu
230 Guest login ok, access restrictions apply.
FTP>
```

After the login process is completed, you see the prompt FTP>, indicating the remote system is ready to accept commands.

When you log on to some systems, you may see a short message containing instructions for downloading files, explaining any restrictions that are placed on anonymous FTP users, or information about the location of useful files. For example, you may see messages like this (taken from the Linux FTP site):

```
To get a binary file, type:  BINARY and then:  GET "File.Name"  newfilename
To get a text file, type:  ASCII  and then:  GET "File.Name"  newfilename
Names MUST match upper, lower case exactly. Use the "quotes" as shown.
To get a directory, type:  DIR. To change directory, type:  CD "Dir.Name"
To read a short text file, type:  GET "File.Name"  TT
For more, type HELP or see FAQ in gopher.
To quit, type EXIT or Control-Z.
```

```
230- If you email to info@sunsite.unc.edu you will be sent help
*information
230- about how to use the different services sunsite provides.
```

We use the warchive experimental ftpd. if you "get" <directory>.tar.Z or <file>.Z it will compress and/or tar it on the fly. Using ".gz" instead of ".Z" will use the GNU zip (/pub/gnu/gzip*) instead, a superior compression method.

Most anonymous FTP sites are set to read-only and do not allow you to upload files (put files) to them. You are usually very restricted regarding where you can go in their file system, too.

## Trivial File Transfer Protocol (TFTP)

The Trivial File Transfer Protocol (TFTP) differs from FTP in two primary ways: it does not log on to the remote machine and it uses the User Datagram Protocol (UDP) connectionless transport protocol instead of TCP. TFTP is usually not used for file transfers between machines where FTP can be used instead, although TFTP is useful when a diskless terminal or workstation is involved. Typically, TFTP is used when a file is requested from a very busy server or when it can be delivered at any time. Using TFTP is much like using email: you send a message asking for a file, and eventually the file arrives back on your system.

TFTP handles access and file permissions by imposing restraints of its own. On most systems a file can be transferred using TFTP only if it is accessible to all users. Because of lax access regulations, most system administrators impose more control over TFTP or ban its use altogether.

The main instructions from the TFTP command set are shown in Table 15.2. Although they appear similar to the FTP command set, they differ in several important aspects because of the connectionless aspect of the TFTP protocol. Most noticeable is the connect command, which simply determines the remote's address instead of initiating a connection.

TABLE 15.2. TFTP'S COMMAND SET.

| TFTP Command | Description |
| :--- | :--- |
| binary | Use binary mode for transfers |
| connect | Determine the remote's address |
| get | Retrieve a file from the remote |
| put | Transfer a file to the remote |
| trace | Display protocol codes |
| verbose | Display all information |

TFTP enables both text and binary transfers. As with both Telnet and FTP, TFTP uses a server process (tftpd on a UNIX system) and an executable, usually called tftp. Because of the nature of TFTP, Windows and similar PC-based operating systems don't usually support it. In most cases, TFTP is used between UNIX machines.

A sample character-based TFTP session is shown here, with full trace options and binary transfers turned on:

```
> tftp
tftp> connect tpci_hpw54
tftp> trace
Packet tracing on.
tftp> binary
Binary mode on.
tftp> verbose
Verbose mode on.
tftp> status
Connected to tpci_hpw54.
Mode: octet Verbose: on Tracing: on
Rexmt-interval: 5 seconds, Max-timeout: 25 seconds
tftp> get /usr/rmaclean/docs/draft1
getting from tpci_hpw54:/usr/rmaclean/docs/draft1 to /tmp/draft1 [octet]
sent RRQ <file=/usr/rmaclean/docs/draft1, mode=octet>
received DATA <block1, 512 bytes>
send ACK <block=1>
received DATA <block2, 512 bytes>
send ACK <block=3>
received DATA <block4, 128 bytes>
send ACK <block=3>
Received 1152 bytes in 0.2 second [46000 bits/s]
tftp> quit
```

You may have to use TFTP in some cases where network conditions are bad or the server doesn't accept standard FTP. Usually, though, FTP should be your choice of protocol.

## Using Telnet

Telnet gives you the capability to log into a remote server and act as though you were physically attached to that machine and all its resources. If the server has a powerful CPU, you can use that CPU instead of your weaker local processor. If the server has some special devices, such as a scanner, CD-writer, or magneto-optical storage device, you can use them. You can also use the remote server's file system.

Using Telnet is quite simple because the protocol takes care of all the configuration and setup processes for you. As part of its startup, Telnet passes a series of messages between the client and server that establish the terminal identifications and special features your
