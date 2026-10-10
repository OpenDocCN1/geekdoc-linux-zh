If you choose to run FreeBSD as a workstation OS, pay particular attention to Part V of this book. If you are configuring a network for the use of many employees, students, or the like, you also should attend to issues surrounding the default GUI configuration, as described in Chapter 23. These environments have matured substantially since the mid-1990s, and are still improving at a rapid rate.

# FreeBSD as a Server OS

A *server* is the second major role for FreeBSD. Servers are computers that have network connections and that respond to requests from other networked computers for data exchanges. This rather dry definition hides the fact that servers underlie the utility of networks. Examples of servers include

+   ■ **File servers**	These computers enable other computers to read files from or upload files to the file server system. They can be used to distribute publicly available files (such as those that make up FreeBSD itself) or as centralized holding areas for files on a local network.

+   ■ **Web servers**	In some sense, web servers are just a *specialized form* of file server. The popularity of web servers means that they deserve special attention, though. They typically deliver files from the server for display in a web client program, better known as a *web browser*.

+   ■ **Mail servers**	A mail server is a computer that exchanges e-mail messages with other mail servers or with end-user mail programs. Most e-mail exchanges on the Internet at large involve at least two mail server computers, but local mail exchanges can use just one mail server.

+   ■ **Login servers**	You can configure a FreeBSD system to accept logins from remote locations. When so configured, the system can be used in a workstation-like way, but from a distance. In some sense, this configuration blurs the line between workstation and server because the networking functions make the system a server, but it’s often used as if it were a workstation. (In some cases, these features may be used on a server computer to enable remote remote administration, as well.)

+   ■ **Miscellaneous servers**	There are server computers that provide many network support functions, such as the *Dynamic Host Configuration Protocol* (DHCP), used to let one computer configure another’s network settings; and font servers, which deliver font information to workstations.

These server functions are described in more detail in Part IV of this book. As you might guess by this coverage, FreeBSD makes an excellent server OS. Part of the reason for this is that many popular server programs were developed first for UNIX, and FreeBSD runs these UNIX servers very well. Coupled with the inexpensive x86 hardware on which FreeBSD runs, FreeBSD can be a very cost-effective way to run many of the world’s most popular server programs.