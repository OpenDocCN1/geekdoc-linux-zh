# Clients

All standard operating systems, such as DOS, Windows, and OS/2, support the SMB protocol. The TCP/IP protocol must be installed on all computers. Samba can also be used with all the various UNIX “flavors”.

SMB servers provide hardware space to their clients by means of shares. Here, a share includes a directory and its subdirectories. It is exported by means of a name and can be accessed by its name. Of course, the share name can be set to any name. It does not have to be the name of the export directory. A printer is also assigned a name. Clients can access the printer by its name.

# Installation and Configuration of the Server

First the package samba from series n should be installed. The SMB services are started when the computer is booted. The services can be started manually with rcsmb start. With rcsmb stop, the services can be stopped.

The main configuration file of Samba is /etc/samba/smb.conf. Here the entire service is configured. It is divided into two separate sections. In the [global] section, the central and general settings are made. The second section is the [share] section. Here the directories are released on a user-dependent basis and the file and directory permissions are set. If a specific value from the [share] section should be made valid for all shares, this can be taken over into the [global] section, making it valid for all shares system-wide. This saves some work for the system administrator. To present a picture of the whole process, an example is displayed in in Files 59 and 60 on page 376. An explanation of it is given afterwards.