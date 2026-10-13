# CERTIFICATION OBJECTIVE 15.01

# Samba Services

Microsoft's CIFS was built on the Server Message Block (SMB) protocol. SMB was developed in the 1980s by IBM, Microsoft, and Intel as a way to share files and printers over a network.

As Microsoft developed SMB into CIFS, the Samba developers have upgraded Samba accordingly. Samba services provide a stable, reliable, fast, and highly compatible file and print sharing service that allows your computer to act as a client, a member server, a Primary Domain Controller (PDC), or a member of an Active Directory (AD) service on Microsoft-based networks. While Samba does not include every feature built into the latest Microsoft networks, I have confidence that it will in the near future.

> I look forward to the final release of Samba 4.0, which will make it possible for Linux to act as an AD controller on a Microsoft-based network. RHEL 6 includes a preliminary version of Samba 4.0 and may include it in the lifetime of RHEL 6.

SMB network communication over a Microsoft-based network is also known as the Network Basic Input/Output System (NetBIOS) over TCP/IP. Through the collective works of Andrew Tridgell and the Samba team, Linux systems provide transparent and reliable SMB support over TCP/IP via a package known as Samba.

Samba emulates many of the advanced network features and functions associated with various Microsoft operating systems through the SMB protocol. Complete information can be found at the official Samba web site at www.samba.org. It is easy to configure Samba to do a number of things on a Microsoft-based network. Here are some examples:

+   - Participate in a Microsoft Windows Workgroup or a domain as a client, member server, or even a PDC.
+   - Share user home directories.
+   - Act as a Windows Internet Name Service (WINS) client or server.
+   - Link to or manage a workgroup browse service.
+   - Act as a master browser.

![](bbox=[0.1, 0.48, 0.2, 0.62])