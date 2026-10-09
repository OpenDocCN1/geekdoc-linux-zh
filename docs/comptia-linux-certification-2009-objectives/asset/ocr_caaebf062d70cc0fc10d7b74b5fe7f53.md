# The lmhosts File

Samba uses the lmhosts file to resolve NetBIOS names to IP addresses. The structure of this file is similar to the /etc/hosts file, but the hostnames follow NetBIOS naming conventions. The default location of the lmhosts file is same as that of the smb.conf file, that is /etc/samba.

# The smbclient Command

The smbclient command is used to transfer files across a network and view the names of shared resources. The following table lists some options provided by the smbclient command.

| Option | Used To |
| :--- | :--- |
| `-N` | Suppress password prompting. |
| `-L host name` | Specify that the shares from the specified host be displayed. |
| `-s path` | Specify the location of the smb.conf file. |
| `-U user name` | Specify the Samba user name. |

It is also used as a tool for retrieving files. The syntax for retrieving the files is smbclient \/machine/service.

# The nmblookup Command

The nmblookup command is used to resolve the NETBIOS names to IP addresses. The following table lists some of the frequently used nmblookup command options.

| Option | Used To |
| :--- | :--- |
| `-T` | Resolve IP addresses to hostnames. |
| `-s path` | Specify the location of the smb.conf file. |
| `-M` | Locate the master browser. |
| `-S` | Display the node status. |

# The Samba Configuration File

The smb.conf file, which is stored in the /etc/samba directory, is the main configuration file for a Samba service. The initialization script runs from the /etc/init.d/smb file. The smb.conf file is structured similar to the Windows.ini file. This file contains a share definition for every directory or device that needs to be shared. A typical share definition contains the share name, the path of the directory or device that is shared, and other options that allow or deny access to the share. Each share is defined as a section within brackets, with the share name specific to the resource being shared.

![](bbox=[0.05, 0.78, 0.17, 0.84])