A printer page description language that was developed by Hewlett-Packard and is in common use today.

# Portable Document Format（PDF）

A highly compressed document format, based on PostScript, used as a document distribution format that is supported by Web browsers as well as many applications. Adobe also distributes an application called “Acrobat,” which is a PDF reader.

# Page Description Language（PDL）

A language for describing the layout and contents of a printed page. The best-known PDLs are Adobe PostScript and Hewlett-Packard PCL (Printer Control Language), both of which are used to control laser printers.

# PostScript Printer Description（PPD）

PPDs specify and control options supported by PostScript printers, such as duplexing, stapling, and DPI. See also Section 21.1.4. PPD files can be read by printing applications to enable correct PostScript page layout for a particular PostScript printer.

# Remote Procedure Call（RPC）

RPCs are a means for executing network operations. The RPC protocol is independent of transport protocols. RPC does not try to implement any kind of reliability and the application that uses RPCs must be aware of the type of transport protocol underneath RPC. An RPC is like a programmatic jump subroutine over a network. RPCs used in the UNIX environment are specified in RFC 1050. RPC is a powerful technique for constructing distributed, client-server based applications. It is based on extending the notion of conventional, or local procedure calling, so that the called procedure need not exist in the same address space as the calling procedure. The two processes may be on the same system, or they may be on different systems with a network connecting them. By using RPC, programmers of distributed applications avoid the details of the interface with the network. The transport independence of RPC isolates the application from the physical and logical elements of the data communications mechanism and allows the application to use a variety of transports.

# Server Message Block（SMB）

SMB was the original name of the protocol “spoken” by Samba. It was invented in the 1980s by IBM and adopted and extended further by Microsoft. Microsoft renamed the protocol to CIFS during the Internet hype in the 1990s.

# User IDentifier（UID）

The UNIX system user identifier: on older systems a 32-bit unsigned integer, and on newer systems, an unsigned 64-bit integer. The UID is used in UNIX-like operating systems for all user-level access control.

# Universal Naming Convention（UNC）

A syntax for specifying the location of network resources (such as file shares). The UNC syntax was developed in the early days of MS DOS 3.x and is used internally by the SMB protocol.