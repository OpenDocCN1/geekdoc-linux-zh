in the primary smb.conf file. The use of NetBIOS over TCP/IP using only TCP port 139 means that the use of the %L macro is fully enabled. If the smb ports = 139 is not specified (the default is 445 139, or if the value of this parameter is set at 139 445 then the %L macro is not serviceable.

It is possible to host multiple servers, each with their own personality, using port 445 (the NetBIOS-less SMB port), in which case the %U macro can be used to provide separate server identities (by IP Address). Each can have its own security mode. It will be necessary to use the interfaces, bind interfaces only and IP aliases in addition to the netbios name parameters to create the virtual servers. This method is considerably more complex than that using NetBIOS names only using TCP port 139.

Consider an example environment that consists of a standalone, user-mode security Samba server and a read-only Windows 95 file server that has to be replaced. Instead of replacing the Windows 95 machine with a new PC, it is possible to add this server as a read-only anonymous file server that is hosted on the Samba server. Here are some parameters:

The Samba server is called ELASTIC, its workgroup name is ROBINSMEST. The CDROM server is called CDSERVER and its workgroup is ARTSDEPT. A possible implementation is shown here:

The smb.conf file for the master server is shown in Example 33.1.1. This file is placed in the /etc/samba directory. Only the nmbd and the smbd daemons are needed. When started the server will appear in Windows Network Neighbourhood as the machine ELASTIC under the workgroup ROBINSMEST. It is helpful if Windows clients that must access this server are also in the workgroup ROBINSMEST as this will make browsing much more reliable.

The configuration file for the CDROM server is listed in Example 33.1.2. This file is called smb-cdserver.conf and it should be located in the /etc/samba directory. Machines that are in the workgroup ARTSDEPT will be able to browse this server freely.

The two servers have different resources and are in separate workgroups. The server ELASTIC can only be accessed by users who have an appropriate account on the host system. All users will be able to access the CDROM data that is stored in the /export/cddata directory. File system permissions should set so that the other user has read-only access to the directory and its contents. The files can be owned by root (any user other than the nobody account).

# 33.1.3 Multiple Virtual Server Hosting

In this example, the requirement is for a primary domain controller for the domain called MIDEARTH. The PDC will be called MERLIN. An extra machine called SAURON is required. Each machine will have only its own shares. Both machines belong to the same domain/- workgroup.

The master smb.conf file is shown in Example 33.1.3. The two files that specify the share information for each server are shown in Example 33.1.4, and Example 33.1.5. All three files are locate in the /etc/samba directory.