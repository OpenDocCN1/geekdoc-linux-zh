+   ☐ RFC-1002 March 1987 Protocol Standard For a NetBIOS Service on a TCP/UDP Transport: Detailed Specifications

RFC-1001 is very readable and explains the ideas behind the implementation. RFC-1002 gives very low-level specifications of packet formats, etc. and you'll probably never want to look at it. Interestingly, Microsoft's own NT implementation doesn't conform 100% to these specs: in particular the NetBIOS Datagram Distribution (NBDD) service doesn't exist.

For an overview of Microsoft's implementation of TCP/IP:

+   ☐ ftp://ftp.microsoft.com/bussys/winnt/winnt-docs/papers/tcpimp2.exe Microsoft Windows NT 3.5/3.5.1/4.0: TCP/IP Implementation Details. TCP/IP Protocol Stack and Services, Version 2.0

We've found Microsoft's own publications to be the best source of detailed information on Windows Networking. In particular, the Resource Kits for the various operating systems contain in-depth (although not comprehensive) discussions on many aspects of Windows Networking. The paper editions of the Resource Kits (which you can buy from a bookstore) contain both the printed manuals and many extra software tools. We've found these tools very useful in understanding how things really work.

+   ☐ Microsoft Windows NT Server resource kit for Windows NT Server version 4.0 (1996, Microsoft Press) (which we refer to from now on as "the Resource Kit.")

The Resource Kit documents are available online. The NT 4.0 version is:

+   ☐ http://www.microsoft.com/technet/prodtechnol/winntas/reskit/default.asp

For higher-level (less nitty-gritty) documents, the Windows NT Server Concepts and Planning Guide is good:

+   ☐ http://www.microsoft.com/technet/prodtechnol/winntas/proddocs/concept/front.asp

(We often have difficulty finding this if we don't have the full URL to hand. On the Microsoft TechNet site, follow the links: TechNet > Products and Technologies > Windows NT Server > Product Documentation.)

Other useful sources of information are the Microsoft TechNet site in general:

+   ☐ http://www.microsoft.com/technet/

and the Microsoft Knowledgebase:

+   ☐ http://support.microsoft.com

which is a database of technical notes, usually relating to bugs or other problems. (The Knowledgebase articles are occasionally reviewed and updated, so unlike the RFCs, you can't use them to trace the history of a feature and see what influenced its development over time.) The Knowledgebase is excellent for very specific questions ("your Windows XYZ system misbehaves when ABC; to work around that …"). However, on all the Microsoft sites we've found it hard to locate articles that provide an overview of a technology area but are still technically oriented. For that type of information we've found the third-party "NT FAQ" site:

+   ☐ http://www.ntfaq.com