ACCEPT SERVICE=X REMOTEIP=127.0.0.1/255.0.0.0

REJECT SERVICE=X NOT REMOTEIP=192.168.98.0/255.255.255

or

ACCEPT SERVICE=X REMOTEHOST=localhost

REJECT SERVICE=X NOT REMOTEHOST=*.threeroomco.com

These examples block connections that do not originate from the 192.168.98.0 IP block or from the threeroom.com domain, respectively, while still allowing connections from the server itself. You can do much more with the lpd.perms file than you can with the old-style lpd's hosts. lpd file. For instance, you can allow or deny access based on the remote user, and you can allow or deny users or machines access to specific LPRng features. The default lpd.perms file contains many examples, so it's well worth examining if you want to fine-tune your configuration.

> NOTE Although LPRng leaves your printer server open to outsiders' printing on by default, its more sophisticated security features make it a more secure printing-package if you configure properly.

# When Windows Is Involved

Things get a bit more complicated when either the local or the destination machine is running some version of Microsoft Windows. Windows printers use a protocol called the Server Message Block (SMB), renamed the Common Internet File System (CIFS), to provide shared printing. Trying to get Windows and Linux computers to share printers using their native tools is like trying to get two people who don't understand the same language to have a conversation. Fortunately, Linux includes a package that teaches Linux to “speak” the Windows file and printer sharing language of SMB/CIFS.

Samba is an important tool for mixed networks that is the subject of a companion volume in the Craig Hunt Linux Library, Roderick W. Smith's Linux Server Administration (Syex, 2001). There's a brief introduction to Samba in Chapter 15 of this book. Briefly, Samba is an open source software that provides SMB/CIFS file and print services to clients that might be running any version of Windows, OS/2, or other OS. Samba runs on Linux, other versions of Unix, MacOS, and other OS. Other sources of information about Samba include an excellent SMB-HOWTO and how Samba lists. The main Samba Web page is http://www.samba.org.

Since we're dealing with printing in this chapter, the next sections show how to configure Samba to print from a Windows machine to a printer attached to a Linux box and from a Linux machine to a printer attached to a Windows machine.