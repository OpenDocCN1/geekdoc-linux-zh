
## Clients and Servers

- Explains how to use TCP wrappers to control who can access a server.
- Explains how to set up and use the most popular Linux servers, providing a chapter on each: Apache; Samba; OpenSSH; sendmail; DNS; NFS; FTP; firewall-config, firewall, and iptables; and NIS/LDAP.
- Describes how to set up a CUPS printer server.
- Explains how to set up and use a MariaDB/MySQL relational database.
- Describes how to set up and use a DHCP server.

## Programming

- Provides a chapter on the Python programming language and a full chapter covering shell programming using bash, including many examples.

## DETAILS

**Chapter 1** presents a brief history of Linux and explains some of the features that make it a cutting-edge operating system.

**Part I**, “Installing Fedora and Red Hat Enterprise Linux,” discusses how to install Fedora/RHEL Linux. **Chapter 2** presents an overview of the process of installing Fedora/RHEL Linux, including hardware requirements, downloading and burning or writing the installation medium, and planning the layout of the hard disk. The “Conventions Used in This Book” section on page 26 details the typefaces and terminology used in this book. **Chapter 3** is a step-by-step guide to installing Fedora and RHEL; it covers installing from an Install Image and from a live session (Fedora).

**Part II**, “Using Fedora and Red Hat Enterprise Linux,” familiarizes you with Fedora/RHEL, covering logging in, the GUI, utilities, the filesystem, and the shell. **Chapter 4** introduces desktop features; describes configuring the system using the Settings window; explains how to use the Nautilus File Browser to manage files, run programs, and connect to FTP and HTTP servers; covers finding documentation, dealing with login problems, and using the window manager; and presents some suggestions on where to find documentation, including manuals, tutorials, software notes, and HOWTOs. The introduction to the command line includes information on terminal emulators, virtual consoles, correcting mistakes on the command line, a few basic utilities, and how to write and execute a simple shell script. **Chapter 5** introduces the Bourne Again Shell (bash) and discusses command-line arguments and options, redirecting input to and output from commands, running programs in the background, and using the shell to generate and expand filenames. **Chapter 6** discusses the Linux hierarchical filesystem, covering files, filenames, pathname, working with directories, access permissions, and hard and symbolic links. **Chapter 7** provides in-depth coverage of 32 useful utilities, and presents tutorials on the vim and nano text editors. **Chapter 8** explains networks, network security, and the Internet, and discusses types of networks, subnets, protocols, addresses, hostnames, and various network utilities. A section covers the all-important IPv6 protocol. The section on distributed computing describes the client/server model and some of the servers you can use on a network. (Details of setting up and using clients and servers are reserved until Part IV)

### Experienced users may want to skim Part II

**tip** If you have used a UNIX or Linux system before, you may want to skim or skip some or all of the chapters in Part II. Do not skip “Conventions Used in This Book” (page 26), which explains the typographic and layout conventions used in this book. Both “Getting Help” (page 113), which explains how to get help using a GUI, and “Getting Help from the Command Line” (page 128), point out both local and remote sources of Linux and Fedora/RHEL documentation.

**Part III** “System Administration,” goes into more detail about administering the system. **Chapter 9** extends the bash coverage from Chapter 5, explaining how to redirect error output, avoid overwriting files, and work with job control, processes, start files, important shell builtin commands, parameters, shell variables, and aliases. **Chapter 10** discusses core concepts, such as the use of su and sudo; working with root privileges; SELinux (Security-Enhanced Linux); system operation, including a discussion of the systemd init daemon; chroot jails; TCP wrappers; general information about how to set up a server; DHCP; and PAM. **Chapter 11** explains the Linux file-system, going into detail about types of files, including special (device) files; the use of fsck to verify the integrity of and repair filesystems; the use of tune2fs to change file-system parameters; and the XFS filesystem and related utilities. **Chapter 12** explains how to keep a system up-to-date by downloading software from the Internet and installing it, including examples that use yum to perform these tasks. It also covers the RPM software packaging system and the use of the rpm utility. Finally, it explains how to use BitTorrent from the command line to download files. **Chapter 13** explains how to set up the CUPS printing system so you can print on both local and remote systems. **Chapter 14** details customizing and building a Linux kernel and includes information on GRUB 2. **Chapter 15** covers additional administration tasks, including setting up user accounts, backing up files, scheduling automated tasks, tracking disk usage, and solving general problems. **Chapter 16** explains how to set up a local area network (LAN), including both hardware (including wireless) and software configuration, and how to set up Cacti to monitor the network. **Chapter 17** describes VMs (virtual machines), how to set up and work with VMs, and how to work with VMs in the cloud.

**Part IV** goes into detail about setting up and running servers and connecting to them using clients. Where appropriate, these chapters include JumpStart sections, which get you off to a quick start in using clients and setting up servers. The chapters in Part IV cover the following clients/servers:

- **OpenSSH**—Set up an OpenSSH server and use ssh, scp, and sftp to communicate securely over the Internet.
- **FTP**—Set up a vsftpd secure FTP server and use any of several FTP clients to exchange files with the server.
- **Email**—Configure sendmail and use Webmail, POP3, or IMAP to retrieve email; use SpamAssassin to combat spam.
- **NIS and LDAP**—Set up NIS to facilitate system administration of a LAN and LDAP to maintain databases.
- **NFS**—Share filesystems between systems on a network.
- **Samba**—Share filesystems and printers between Windows and Linux systems.
- **DNS/BIND**—Set up a domain nameserver to let other systems on the Internet know the names and IP addresses of local systems they may need to contact.
- **firewalld, firewall-config, and iptables**—Set up a firewall to protect local systems and share a single Internet connection between systems on a LAN.
- **Apache**—Set up an HTTP server that serves Web pages, which browsers can then display. This chapter includes many suggestions for increasing Apache security.

**Part V** covers three important programming tools that are used extensively in Fedora/RHEL system administration and general-purpose programming. **Chapter 27** continues where Chapter 9 left off, going into greater depth about shell programming using bash, with the discussion enhanced by extensive examples. **Chapter 28** introduces the flexible and friendly Python programming language, including coverage of lists and dictionaries, using libraries, defining functions, regular expressions, and list comprehensions. **Chapter 29** covers the widely used MariaDB/MySQL RDBMS (relational database management system), including installation, creating a database, adding a user, creating and modifying tables, joins, and adding data to the database.

**Part VI** includes appendices on regular expressions, helpful Web sites, system security including GPG, updating software using apt-get, and a map that indexes LPI's Linux Essentials certification learning goals and CompTIA's Linux+ exam objectives to the pages in this book that cover each topic. This part also includes an extensive Glossary with more than 500 entries plus the JumpStart index, the File Tree index, the Utility index, and the comprehensive Main index.

## SUPPLEMENTS

The author's home page (www.sobell.com) contains downloadable listings of the longer programs from this book, as well as pointers to many interesting and useful Linux sites on the World Wide Web, a list of corrections to the book, answers to even-numbered exercises, and a solicitation for corrections, comments, and suggestions.

## THANKS

First and foremost, I want to thank Mark L. Taub, Editor-in-Chief, Prentice Hall, who provided encouragement and support through the hard parts of this project. Mark is unique in my 30+ years of book writing experience; an editor who works with the tools I write about. Because Mark runs Linux on his home computer, we
