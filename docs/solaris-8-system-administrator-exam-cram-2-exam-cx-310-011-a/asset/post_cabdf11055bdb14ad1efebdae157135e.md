
### **syslog priority levels**

A syslog message can be identified by priority level or severity. This identification provides a second mechanism (with finer granularity) for handling messages on the basis of importance.

### **syslog source facilities**

The facilities generating syslog messages can be used to determine where the messages are sent or stored. Doing so allows separate log files for different types of messages based on source.

### **system configuration phase**

The installation phase during which basic information about the system, such as hostname and domain, is identified. This information can optionally be set up ahead of time (preconfigured).

### **system installation phase**

The installation phase during which the system software is installed. The system software is one of the Solaris 8 software groups.

### **system profile**

For user accounts that use sh (Bourne shell) or ksh (Korn shell) as a login shell, commands in the system profile (/etc/profile) are executed before the user’s login initialization file.

### **system run levels**

Eight defined levels, each associated with specific functions used to shut down or reboot the system and control system services and resources.

### **Transmission Control Protocol/Internet Protocol (TCP/IP) Network Model**

A network model consisting of five layers of services. Each layer is responsible for handling a different aspect of network communication.

### **UFS file system logging**

Updates to a UFS file system are recorded in a log before they are applied. In the case of system failure, the system can be restarted, and the UFS file system can quickly use the log instead of having to use the fsck command.

### **user account**

A unique name and user ID that control an individual’s access to a computer and its resources.

### **user ID (UID)**

A unique numeric ID assigned to a user account that is used for file and process ownership and access permissions.

### **Veritas File System (vxfs)**

The type of virtual file system that Enterprise Volume Manager supports.

### **virtual disk management system**

A software package that allows the use of physical disks in ways that the standard Solaris file systems do not support. It can overcome disk capacity and architecture limitations and improve performance and reliability. In addition, the use of a graphical management tool enhances manageability.

### **virtual file system**

An enhanced file system that provides improved performance and data reliability.

### **volume**

An Enterprise Volume Manager virtual disk device composed of up to 32 plexes. The volume is the virtual object that the operating system and applications view and manipulate.

### **Volume Manager (VM) disk**

A physical disk partition or slice that has been assigned to Enterprise Volume Manager.

### **volume table of contents (VTOC)**

Contains the partition table and geometry data about the disk, such as sectors per track, tracks per cylinder, available cylinders, and so on.

### **WebNFS**

A protocol that allows Web browsers to access NFS resources. RFCs 2054 and 2055 define this protocol.

### **Web Start**

An interactive installation method that uses a Web browser interface.

### **x86 Intel compatible**

A computer architecture based on a microprocessor originally designed by the Intel Corporation, which used the 286, 386, 486 series of numbers to denote versions.

### **X/Open Federated Naming Specification (XFN)**

The specification for the Federated Naming Service (FNS) as defined by the X/Open Consortium.

### **zone**

A portion of a domain delegated to a DNS server.

## Index

### Symbols

- . (dot), file and directory names with, 221
- /etc/auto_master file, 365
- /etc/dfs/dfstab file, 358–359
- /etc/group file, 94–95
- /etc/hostname file, 282
- /etc/inet/hosts file, 281
- /etc/mnttab file, 192
- /etc/nodename file, 281
- /etc/nsswitch.conf file (name service switch), 382–386
- /etc/nsswitch.nisplus file (listing 19.1), 385–386
- /etc/passwd file, 92–93
- /etc/shadow file, 94
- /etc/syslog.conf file, 300
- /etc/vfstab file, 191–192, 361–362
- $HOME/.profile
    - defining shell variables in, 132–133
    - sourcing, 133
- /usr file system, restoring, 205

### A

- accounts
    - administrative accounts (superuser), 90
        - restricting, 90–92
        - sysadmin group, 92
    - group accounts, 122
        - administration files, 92–95
        - changing file ownership, 104–105
        - creating, 122–124
        - deleting, 123–124
        - modifying, 123–124
    - user accounts, 90, 116
        - administration files, 92–95
        - changing file ownership, 103–104
        - creating, 116–121
        - deleting, 119, 122
        - identifying and monitoring, 134–137
        - initialization files, 129–133
        - locking with admintool command, 128
        - login procedures, 133–134
        - logout procedures, 134
        - modifying, 119, 121–122
        - passwords, 121
        - remote authentication database, 232–233
        - sysadmin group, 92
- ACLs (Access Control Lists), 100–101
    - displaying with getfacl command, 102–103
    - setting with setfacl command, 101–102
- actions (syslog facility), 298
- Address Resolution Protocol (ARP), 279–280
- addresses
    - Ethernet, 279
    - IP, 279
        - converting hostnames to, 281
- add_install_client command, 418-421
    - command-line arguments, 419-420
- add_to_install_server command, 417
- administration files for user and group accounts, 92
    - /etc/group file, 94–95
    - /etc/passwd file, 92–93
    - /etc/shadow file, 94
- administrative accounts, 90
    - superuser, 90
        - restricting, 90–92
        - sysadmin group, 92
- AdminSuite, 401
    - Database Manager, 403
    - Group Manager, 405
    - Host Manager, 401–402
    - Printer Manager, 405
    - Serial Port Manager, 404
    - Storage Manager, 402–403
    - User Manager, 404–405
- admintool command, 46, 116, 119, 122–124, 401
    - group accounts
        - creating, 122–123
        - deleting, 123
        - modifying, 123
    - passwords, changing, 126–127
    - software packages
        - deleting, 52–53
        - displaying information, 51
        - installing, 48–50
    - sysadmin group, 92
    - user accounts
        - creating, 116–118
        - deleting, 119
        - locking, 128
        - modifying, 119
- advertising. *See* sharing
- aliases (OpenBoot), 70
    - creating, 71
    - deleting, 72
    - displaying, 71–72
- answer key to sample exams, 260–272, 450–463
- answering questions, tips for, 11, 241–244
- Application OSI layer, 277
- Application TCP/IP layer, 278
- archiving. *See* backing up
