Then, in the directory /home/ftp/pub/kickstart, place the kickstart files, which must have names of the form xxx.xxx.xxx.xxx-kickstart, xxx.xxx.xxx.xxx is the IP address of the client system.

When the installation program fetches the kickstart file via DHCP, it assumes it should perform a network installation from an NFS server. By default, it tries to mount an NFS directory exported by the same host that answered the DHCP query. If you want to use a different host to serve the NFS requests, include the following directive in /etc/dhcpcd.conf file:

```
next-server nfserver;
```

where nfsver is the host name or IP of the desired NFS server on which the kickstart file resides. To give the location of installation media, you can specify a kickstart directive of the form

```
nfs --server server directory
```

where server specifies the NFS server and directory specifies the NFS-exported directory.

For further information on setting up a DHCP server, see Chapter 23, “Understanding Secondary Network Services."

# Performing the Kickstart Installation

To start the kickstart installation, specify the ks argument at the linux prompt. Use the command

```
linux ks
```

if the kickstart file is to be obtained from a DHCP or NFS server. Use the command

```
linux ks=floppy
```

if the kickstart file resides on the root directory of the boot floppy disk. If the kickstart installation needs information that it cannot find in a kickstart directive, it prompts for the information using the dialog box presented by a non-kickstart installation.