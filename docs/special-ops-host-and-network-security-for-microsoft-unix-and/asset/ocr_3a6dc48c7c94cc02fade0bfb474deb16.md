# Chapter 7 • Securing Exchange and Outlook Web Access

SMTP queues, gobble up WAN bandwidth, take up inbound queue disk space, generate gigabytes of transaction logs, and overwhelm global catalog servers. If an organization has mail-enabled contacts from customers, vendors, or other external organizations, these e-mail-based viruses will be sent to users as well.

In my largest customers, e-mail viruses contribute to loss of service far more than server crashes, database corruption, or other hardware failures.

# Types of File Vulnerabilities

Exchange 2000 has a couple of sneaky vulnerabilities that administrators never realize: information store file vulnerabilities and message tracking logs. Both require access to either the Exchange server, the network, or to the server’s backup in order to exploit. These are files in the data can be easily viewed and possibly used to some nefarious purpose.

# Information Store File Vulnerabilities

An exploit of the information store file requires physical access to the backup tapes or the server console. Exchange information stores are broken into two separate files. The first of these is called the MAPI store (a.k.a. the rich text store). All messages received their message header information stored in this file; messages from MAPI have their message bodies and attachments stored in this file as well. The format of the message is called Message Database Encoding Format (MDEF); the information is encoded and not easily readable, but impossible to read. A creative intruder with a hex editor or database tools may allow to view the data in the EDB file.

The real vulnerability is the other database file; this is known as the streaming file or the native content store. When messages are received from SMTP clients, HTTP clients, NNTP clients, or through the file system (ExtISFS), the message body and attachment is stored in this file in the exact format in which it was transmitted. This reduces the Exchange server’s overhead by converting data as necessary. This file can be retrieved in Notepad or any other text viewing program, and the entire contents can be viewed.

# Message Tracking Logs

The message tracking facility allows an administrator to view which components and servers have touched an internal e-mail message. This can be useful in locating a stalled message or determining the path that message took to