
# Book VI: System Administration
(推断：基于章节编号和主题连续性，此处可能缺失了Book VI的标题，但根据OCR内容，从Chapter 2开始是用户管理，通常属于系统管理部分。不过为了忠实于原文，仅处理可见标题。原文Page 19开始直接是Chapter 2，Page 20有Chapter 5, 6，Page 21有Book VII。因此Page 19-20的内容属于前一本书或同一本书的前几章。由于没有明确的Book VI标题，我将按照章节层级处理。)

## Chapter 2: Managing Users
- Adding User Accounts
  - Using the User Manager to add user accounts
  - Using commands to manage user accounts
- Understanding the /etc/passwd File
- Managing Groups
- Exploring the User Environment
- Changing User and Group Ownership of Files

## Chapter 3: Managing the File System
- Learning the Linux File System
  - Understanding the file-system hierarchy
  - Mounting a device on the file system
  - Examining the /etc/fstab file
- Sharing Files with NFS
  - Exporting a file system with NFS
  - Mounting an NFS file system
- Backing Up and Restoring Files
  - Selecting a backup strategy and media
  - Commercial backup utilities for Linux
  - Using the tape archiver — tar
- Accessing DOS/Windows File Systems
  - Mounting a DOS disk partition
  - Mounting DOS floppy disks
  - Mounting an NTFS Partition
- Using mtools
  - Trying mtools
  - Understanding the /etc/mtools conf file
  - Learning the mtools commands
- Formatting a DOS floppy

## Chapter 4: Managing Applications
- Working with Red Hat Package Manager
  - Using the RPM commands
  - Understanding RPM filenames
  - Finding out about RPMs
  - Installing an RPM
  - Removing an RPM
  - Upgrading an RPM
  - Verifying an RPM
- Building Software Packages from Source Files
  - Downloading and unpacking the software
  - Building the software from source files
  - Installing SRPMs
- Updating Fedora Core Applications with Up2date
- Using Yellow Dog Updater, Modified (Yum)

## Chapter 5: Managing Devices and Printers
- Understanding Linux Devices
  - Device files
  - Persistent device naming with udev
  - Managing Loadable Driver Modules
    - Loading and unloading modules
    - Using the /etc/modprobe.conf file
- Managing USB Devices
- Managing Print Queues in Fedora Core
  - Spooling and print jobs
  - Printing with the lp command
  - Checking the print queue using lpq
  - Canceling the print job using cancel
  - Checking the printer status using lpstat
  - Controlling the print queue

## Chapter 6: Upgrading and Customizing the Kernel
- Upgrading with a Kernel RPM
  - Downloading new kernel RPMs
  - Installing the kernel RPMs
  - Trying out the new kernel
- Rebuilding the Kernel
  - Creating a monolithic versus a modular kernel
  - Configuring the kernel
    - Running the kernel configuration tool
- Building the Kernel and the Modules
- Installing the Modules
- Creating the Initial RAM Disk File
- Installing the New Kernel and Setting Up GRUB
- Rebooting the System

# Book VII: Security

## Chapter 1: Understanding Network and Host Security
- Why Worry About Security?
- Establishing a Security Framework
  - Determine business requirements for security
  - Perform risk analysis
  - Establish security policy
  - Implement security solutions (mitigation)
  - Manage security
- Securing Linux
  - Understanding the host security issues
  - Understanding network security issues
- Learning Computer Security Terminology
- Keeping Up with Security News and Updates

## Chapter 2: Securing the Host
- Installing Operating System Updates
- Securing Passwords
  - Shadow passwords
  - Pluggable authentication modules (PAMs)
- Protecting Files and Directories
  - Viewing ownerships and permissions
  - Changing file ownerships
  - Changing file permissions
  - Setting default permission
  - Checking for set user ID permission
- Using exec-shield
- Using SELinux
- Encrypting and Signing Files with GnuPG
  - Understanding public-key encryption
  - Understanding digital signatures
  - Using GPG
- Monitoring System Security

## Chapter 3: Securing the Network
- Securing Internet Services
  - Using chkconfig to disable standalone services
  - Configuring the xinetd server to disable services
- Using Secure Shell (SSH) for Remote Logins
- Setting Up Simple Firewalls
  - Screening the router with packet filtering
  - Dual-homed host
  - Perimeter network with bastion host
  - Application gateway
- Enabling Packet Filtering on Your Fedora Core System
  - Using the security level configuration tool
  - Using the iptables command

## Chapter 4: Performing Security Audits
- Understanding Security Audits
  - Nontechnical aspects of security audits
  - Technical aspects of security audits
- Learning a Security Test Methodology
  - Some common computer vulnerabilities
  - Host security review
  - Network-security review
- Exploring Security Testing Tools
  - Nmap
  - Nessus
  - SAINT
  - SARA

# Book VIII: Internet Servers

## Chapter 1: Managing the Servers
- Understanding Internet Services
  - TCP/IP and sockets
  - Internet services and port numbers
- Using the inetd Super Server
- Running Standalone Servers
  - Starting and stopping servers manually
  - Starting servers automatically at boot time

## Chapter 2: Running the Apache Web Server
- Exploring HTTP
- Exploring the Apache Web Server
  - Installing the Apache Web server
  - Starting the Apache Web server
- Configuring the Apache Web Server
  - Using Apache configuration tools
  - Apache configuration files
    - The httpd.conf configuration file
    - Virtual host setup

## Chapter 3: Setting Up the FTP Server
- Installing the FTP Server
- Configuring the FTP Server
  - vsftpd configuration files
    - /etc/vsftpd/vsftpd.conf file
    - /etc/vsftpd.ftpassers file
    - /etc/vsftpd.user_list file
- Setting Up Secure Anonymous FTP
- Trying Anonymous FTP
  - Key features of anonymous FTP

## Chapter 4: Serving Up Mail and News
- Installing the Mail Server
  - Using sendmail
    - A mail-delivery test
    - The mail-delivery mechanism
    - The sendmail configuration file
      - sendmail.cf file syntax
    - Other sendmail files
      - The .forward file
      - Invoking procmail in the .forward file
    - The sendmail alias file
- Installing the News Server
  - Configuring and Starting the INN Server
    - InterNetNews components
      - The incoming.conf file
      - The readers.conf file
    - InterNetNews startup
  - Setting Up Local Newsgroups
    - Defining a newsgroup hierarchy
    - Updating configuration files
    - Adding the newsgroups
    - Testing your newsgroups

## Chapter 5: Setting Up DNS
- Understanding Domain Name System (DNS)
  - What is DNS?
  - Learning hierarchical domain names
  - Exploring Berkeley Internet Name Domain (BIND)
- Configuring DNS
  - Configuring the resolver
  - Configuring a caching name server
  - Configuring a primary name server

## Chapter 6: Running Samba and NFS
- Sharing Files with NFS
  - Exporting a file system with NFS
  - Mounting an NFS file system
  - Using the NFS Server Configuration tool
- Setting Up a Windows Server Using Samba
  - Checking whether Samba is installed
  - Configuring Samba
  - Trying out Samba
