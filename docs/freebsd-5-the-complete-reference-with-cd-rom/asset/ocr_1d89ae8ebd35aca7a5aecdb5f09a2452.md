to better enable the server to fit into the client system's filesystem model. For instance, NFS supports UNIX-style permissions and ownership, while SMB/CIFS supports DOS-style hidden, system, and archive attributes. In most respects, though, file transfer and file sharing servers provide similar functionality—namely, the ability to transfer whole files in either direction. (In fact, there are clients to treat FTP as a file-sharing protocol, and Samba ships with a tool called smclient that provides an FTP-like interface on Samba servers.)

# Ancillary File Server Features

In addition to basic file-transfer abilities, file servers support a host of peripheral features. Some of these help define the server as falling in the file transfer or file sharing category, and others help determine the precise role that the server can fill in a network. Examples of such features include

+   * Filename limits Most file server protocols have broad limits on filenames. Many rely upon the host OS for details such as whether filenames are interpreted in a case-sensitive manner.

+   * Ancillary file metadata Some protocols provide for the transfer of various types of file metadata (data that describe the file), such as ownership and permissions. As just noted, in "File Transfer Servers Versus File Sharing Servers," such metadata can be important in file sharing servers because the available metadata should match the metadata supported by the client OS.

+   * File listings When transferring files, it's helpful to be able to see a listing of available files. The three servers described in this chapter all provide such listings, but a few of the more primitive file servers don't; when using them, you must know the names of the files you want to transfer when making the request.

In addition to file server features, client features can be very important. In the case of FTP, a wide variety of clients are available, ranging from the original text-mode ftp to flashy GUI programs. File sharing servers are typically used from tools that are built into the client OSs, and that make the server look like a local hard disk to local applications. Chapter 24 includes information on some common file transfer clients for FreeBSD.

# Common File Servers and Their Uses

Many different file servers exist, and each has its own place in the file server world. Some of the more popular file servers include

+   * FTP Servers As already noted, FTP is an early and still-popular file server protocol. It's implemented in several different servers, such as WU-FTPD, ProFTPD, and BSD FTP. The next section, "Setting Up an FTP Server," describes the operation of BSD FTP in FreeBSD. FTP is useful for general-purpose file-transfer operations when users have accounts on the FTP server system. A special mode, known as anonymous FTP, allows users to transfer files when they don't have accounts. (For security reasons, anonymous FTP is usually configured to