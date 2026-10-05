# Samba installation

Samba not only serves files through CIFS, but it can also perform the basic functions of a Windows Active Directory controller. As a domain controller, Samba supports advanced features such as Windows domain logins, roaming Windows user profiles, and CIFS print spooling.

Most of Samba's functionality is implemented by two daemons, **smbd** and **nmbd**. **smbd** implements file and print services, as well as authentication and authorization. **nmbd** provides the other major CIFS components: name resolution and service announcement.

Unlike NFS, which requires kernel-level support, Samba requires no drivers or kernel modifications and runs entirely as a user process. It binds to the sockets used for CIFS requests and waits for a client to request access to a resource. Once a request has been authenticated, **smbd** forks an instance of itself as the user who is making the requests. As a result, normal file-access permissions (including group permissions) are obeyed. The special functionality that **smbd** adds on top of this is a file-locking service that gives clients locking semantics to how they are accounted.

# Samba installation

Samba is known to work with all of our examples.¹¹ Linux distributions package it as a matter of course. Patches, documentation, and other goodies are available from samba.org. Make sure you are using the most current Samba packages for your system since any updates fix security vulnerabilities.

On all systems, you will need to edit the **smb.conf** file (which is to be found in `/etc/samba/smb.conf` or `/etc/conf`) to tell Samba how to behave. In this file, you specify the directories and printers that will be shared, their access rights, and Samba's general operational parameters. The Samba package comes with a well-commented **smb.conf** file that is a good starting place for new configurations. Note that once Samba is running, it checks its configuration file every few seconds and reloads changes you make.

It's important to be aware of the security implications of sharing files and others over a network. For a typical site, you need to do two things to ensure a basic level of security:

+   * Explicitly specify which clients can access the resources shared by Samba. This part of the configuration is controlled by the **hosts allow** clause in the **smb.conf** file. Make sure that contains only the IP addresses (or ranges) that it should.

+   * Access to the server from outside your organization. Samba uses encryption only for password authentication. It does not use encryption for its data transport. In all cases, you should block access from

+   1. HP also offers a Samba derivative called the HP CIFS Server, which is available for download from the HP software depot.

![](bbox=[0.943, 0.725, 0.996, 0.836])