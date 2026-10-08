# ## Building a Samba File Server

Early in the game, Linux gained much popularity by acting as a file server for both Windows and Linux computers. It did that by dancing the Samba. Samba is more than just a dance routine — it’s a suite of programs that speaks the same file-sharing language (the *protocol*) as Microsoft Windows. Using Samba produces a way to share the Linux file system on a network.

This section describes how to install and configure Samba on your Red Hat Linux computer. Samba comes bundled with Red Hat Linux, of course, so installation is a breeze. Samba is also configured to automatically share the ubiquitous `/home` directory, so configuration is also easy.

![](bbox=[0.12, 0.37, 0.21, 0.44])

Samba is based on the client-server model in which a computer (server) provides services to one or more computers (clients). Samba uses the term *share* (which comes from the Microsoft Windows world) to refer to any object it exports to a network. An object can be a directory or a printer.

# ### Installing and starting Samba

Samba consists of several programs, configuration files, and documentation files. The complete Samba package consists of four RPM files that come bundled on the DVD-ROM accompanying this book. This list describes the purpose of each RPM file:

+   - **samba-client:** This package contains the utility and other supporting software to connect a Linux computer to a Samba server. You can use the interactive utility `smbclient` to connect to a Samba share. The default Red Hat Linux installation installs this package by default.
- **samba:** The Samba server software is included in this package. All the programs for sharing files, directories, and printers are included here; the two essential daemons are `smbd` and `nmbd`; the essential configuration file is `smb.conf`. The utilities for controlling the daemons are also included.
- **samba-swat:** You can manually configure the Samba configuration file, `smb.conf`, if you’re an expert. However, Samba provides a Web-based system that is much easier to use and produces clean and readable configuration files.
- **samba-common:** All the software required by the other three packages is included in this file. This package is also installed by default.