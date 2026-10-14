
are used by their respective operating systems to allow for directory or filesystem sharing.

## NFS

The Network Filesystem allows different operating systems the ability to exchange data transparently. The major components of NFS are the remote procedure call (RPC) and the external data representation (XDR) language. RPCs allow a local machine to request that a remote machine perform a function and return the results of that request. XDR defines data structures in a machine-independent manner. This allows NFS to share directories and filesystems over the network between different operating systems. NFS has become the de facto standard in UNIX operating systems, but it is also available on many other operating systems, including Windows 2000.

## SMB

SMB is the protocol primarily used by Windows 2000 for network connections to files, printers, and resources. The SMB protocol runs on top of TCP/IP, NetBEUI, and IPX/SPX. This versatility allows SMB to function in almost any network environment. There have been several variants to the base SMB protocol over the years, most notably the NTLM protocol used in Windows NT 4.0 and Windows 2000. The latest variant to the SMB protocol is CIFS, or the Common Internet Filesystem. CIFS is NTLM plus a few extras for optimizing performance over the Internet. SMB is a client/server protocol, and is available for many platforms.

## SAMBA

SAMBA provides both client and server SMB services for UNIX systems. SAMBA allows SMB connections to and from most UNIX platforms. With the exception of Linux, none of the standard UNIX systems ship with any SMB service. Red Hat Linux includes a later build of SAMBA. SAMBA has quickly become the foremost SMB service for UNIX systems. The nearest SAMBA mirror site is located at http://www.samba.org. SAMBA is free and not difficult to install.

This chapter explained the concepts, applications, and procedures necessary to share files and directories between computing systems. The next logical step, and an essential part of system administration, is to provide individuals the ability to share information with each other via the computer/network infrastructure. Thus, the next chapter will cover the installation and configuration of electronic mail services.

## ELECTRONIC MAIL AND MESSAGING

## UNIX

- Electronic Mail Protocols
- Sendmail Installing
- Sendmail Configuring
- Testing Sendmail
- Running Sendmail

## WINDOWS 2000

- Microsoft Exchange Server
- Installing Exchange Server 5.5
- Creating Mailboxes
- Creating Distribution Lists
- Exchange 2000 Server

![](img/415c89a1ede71e11e5040a0038b6916c_373_0.png)

Electronic mail is quite possibly the most critical of all services provided on your network. In today's world, businesses depend on electronic mail as much as they depend on electricity or telephones. This chapter provides an overview of Sendmail for UNIX systems and Microsoft Exchange Server for Windows 2000 systems. We intend to provide you with a basic framework that will help you to get started with electronic mail services. A fundamental difference between Sendmail and Exchange 5.5 is the way in which email accounts are created. Email is a direct by-product of a UNIX account. Once the account is created, email is available. In Exchange, however, an email account must be created separately. This difference is reflected in the material presented in this chapter.

## Overview of Electronic Mail

Getting email to its destination requires three basic agents: the Mail Transfer Agent (MTA), the Mail Delivery Agent (MDA), and the Mail User Agent (MUA). These agents work together to send, route, and deliver email to its final destination. To successfully interact, agents must conform to standard protocols. The Internet Engineering Task Force (IETF) administers the official Internet protocol standards for electronic mail. We will briefly explain the agents and standards for electronic mail in the following two sections.

### MAIL AGENTS

The MTA handles the routing of email on the Internet or within your local organization. The MTA performs three primary functions: it routes email to other MTAs, it delivers email to an MDA (Sendmail only) locally, and it accepts email from an MUA. Protocols utilized in the transfer of email are determined through negotiation. The main protocols are the Simple Mail Transfer Protocol (SMTP) and the Extended Simple Mail Transfer Protocol (ESMTP). Sendmail and Exchange are MTAs and will be reviewed later in this chapter.

The MDA handles local delivery of email. The MDA receives email from the MTA and delivers the email to a directory that can be accessed by the MUA. UNIX Sendmail frequently utilizes `/bin/mail` or `procmail` for its MDA. Exchange doesn't utilize an MDA.

The MUA is the user interface to email. It allows the user to edit, view, store, and manipulate email. The MUA is responsible for formatting email in accordance with the standard for the format of ARPA Internet text messages (RFC822). It also “talks” to SMTP/ESMTP with an MTA when it is sending email. The Post Office Protocol (POP) and Internet Message Access Protocol, Version 4rev1 (IMAP4rev1) were developed to transfer email from the mail server to the client for manipulation. We cover the different types of MUAs for UNIX and Windows 2000 clients in the following sections.

### STANDARDS

The official Internet protocol standards for email are contained in requests for comment (RFCs) that are administered by the Internet Engineering Task Force (IETF, http://www.ietf.org). The RFCs listed in Table 9.1 are the current Internet standards for email. Each of these RFCs contains detailed protocol specifications for the exchange of email on the Internet. The mail agents discussed above must conform to these standards to successfully send and receive electronic mail over the Internet. The RFCs dealing with Multipurpose Internet Mail Extensions (MIME, RFC1521 and
