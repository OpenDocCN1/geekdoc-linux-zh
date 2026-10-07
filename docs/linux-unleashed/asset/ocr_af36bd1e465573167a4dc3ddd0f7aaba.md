We use the Warchive experimental ftpd. if you "get" <directory>.tar.Z or <file>.Z it will compress and/or tar it on the fly. Using ".gz" instead of ".Z" will use the GNU zip (/pub/gnu/gzip*) instead, a superior compression method.

Most anonymous FTP sites are set to read-only and do not allow you to upload files (put files) to them. You are usually very restricted regarding where you can go in their file system, too.

# ## Trivial File Transfer Protocol (TFTP)

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