# Installation

Samba is contained in three packages:

+   - samba-common, which contains files needed by Samba clients and servers
- samba, which contains the Samba server
- samba-client, which contains the Samba smclient, smbmount, and smbprint programs and associated files and documentation

Samba is frequently updated; you should consider downloading the latest packages from the Samba Web site, www.samba.org, rather than installing packages contained on Red Hat Linux distribution media.

To install a Samba server, move to the directory containing the packages and issue the command

```
rpm -Uvh samba-*.rpm
```

This command installs both the Samba server and the Samba client, which is helpful in troubleshooting the server. To install only the Samba client, move to the directory containing the packages and issue the command

```
rpm -Uvh samba-common-*.rpm samba-client-*.rpm
```

# Basic Server Configuration

The main Samba configuration file is /etc/smb.conf, which is described in the page smb.conf, in the documentation files residing in /usr/doc/samba* and on the Samba Web site, www.samba.org/docs. The configuration file contains two types of directives:

+   - Global directives, which configure the server
- Service directives, which configure shared files and printers

This section explains the contents of the Samba configuration file. You can use a editor to configure Samba by revising the contents of the file. If you prefer using a graphical tool to configure Samba, you can use linuxconf. Also, the swat package provides a Web-based interface for figuring Samba.

# Samba Global Directives

Here are the global directives contained in a simple Samba configuration:

```
# specify the name of the workday
workgroup = MYGROUP
```