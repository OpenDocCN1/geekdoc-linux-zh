
clients are allocated this number at startup and this number and their frame type are all they need to know in order to access services on the network. Routing in an IPX network is performed by the server, which usually has one network card for each network that they serve. Routing information is shared between servers by means of periodic broadcasts of the routing information using the RIP protocol. Using this protocol, the servers learn the topology of the network shortly after coming up.

## Linux as NetWare Client

Once you have your kernel compiled to support the IPX protocol, you are ready and able to set up your Linux system as a NetWare client. This involves the following steps:

- 1. Loading the ncpfs module.
- 2. Using the IPX tools to get your network number.
- 3. Finding servers on the network.
- 4. Mounting a NetWare volume.
- 5. Configuring your system to use NetWare printers.

The first step is self-explanatory and simply involves issuing the insmod command as follows:

```
insmod ncpfs
```

Once this is done, you are ready to use the IPX tools to get your network number from the server. This is done with the ipx_configure command. For most installations, the command you would use is as follows:

```
ipx_configure --auto_interface=on --auto_primary=on
```

If this works, you can now query the network for a list of servers using the slist command. This command does a broadcast on the network and reports any responses from NetWare servers. If you know the name of your server, you can verify that it is accessible to you by issuing the slist command with either the complete name of the server, or a pattern that will match the name of your server. For example, if your server name is Grumpy, you could issue the following command:

```
slist G*
```

If slist does not find any server on the network, it will respond with a message to that effect.

Once you know the server name, and have verified with slist that you can see it, you can mount NetWare volumes on your Linux client. In order to do this, you will need four pieces of information. They are as follows:

- The fileserver name
- The volume name
- A login id and password on the server
- The mount point where the volume should be mounted

For example, assume that on the server Grumpy, there is a volume named ACCT01 and you want to access it as user guest who has no password. The mount point for this volume will be /nw/acct01. This would mean that you need to issue the following command:

```
ncp mount -S Grumpy -U guest -n V ACCT01 /nw/acct01
```

You can now access the files on the NetWare volume just like any other filesystem on your Linux system.

Once you are configured on the network, other things that you can do include sending messages to NetWare users using the nsend command, and print to NetWare printers. Printing is normally done using the nprint command, but if you prefer a more persistent connection to the printer and want to use the standard print utilities, you can use the PrintTool part of the control-panel to configure the printer for you and a filter will be constructed that issues the appropriate nprint command. Just as with access volumes on a NetWare server, in order to do this you must know the name of the server, the queue name, a login id and password on the server with print permission, and the type of printer attached.

## Linux as NetWare Server

If you choose to make Linux a server in the role of a NetWare server, under Red Hat you will want to run mars_nwe or lward. Both of these products allow Linux to provide NetWare file and print services on to a network of IPX clients. Of these two, the one covered here is the one that comes with your Red Hat distribution, mars_nwe, also known as Martin Stover's NetWare Emulator.

The mars_nwe package implements a subset of the Novell NCP protocol for file-, print-, and disk-based bindery services. This allows Linux to appear to IPX clients as a NetWare server. Assuming that you have the packages installed as noted earlier, let's take a look at the default configuration as supplied by Red Hat. The configuration file for mars_nwe is located in the /etc directory and is called nwserv.conf. As you can see, it is heavily commented. Listing 18.1 contains parts of this configuration file interspersed with explanations that are designed to help you complete the configuration of the mars_nwe package.

### LISTING 18.1 Section 1 from the /etc/nwserv.conf File—Volume Configuration

```
# ============================================================================
# Section 1: volumes (required)
#
# In this section you list all Linux-directories accessible via mars_nwe.
#
# To be more precise: a mapping from Linux-directories to mars_nwe-volumes
# is done. (Volumes are the beasts you can map to drive letters under DOS
# using map.exe ).
#
# Linux-directory          mars_nwe-volume   map.exe      DOS-Drive
# /var/local/nwe/SYS  ......> SYS          ............> W:
#
# More than one entry is allowed in this section.
# The maximum number of volumes is a compile-time option that must be
# specified in 'config.h' before compiling mars_nwe.
#
# Please note that at least the volume SYS must be defined and it must
# contain the following sub-directories: LOGIN, PUBLIC, SYSTEM, MAIL.
# See the installation-instructions in the doc-directory for more infos.
#
# ...................................................................
#
# Syntax:
#   1        VOLUMENAME      DIRECTORY          OPTIONS
#
# VOLUMENAME:  the name of the mars_nwe-volume (max. 8 characters)
# DIRECTORY:   the directory on your Linux-system associated with that
#              volume; use the special name ~ to refer to the users
#              individual home-directory
#
# OPTIONS:     none or some of the following characters (without a seperator)
# k            allow lowercase-filenames (if you don't set this, all
#              files must be upper-case)
# m            removable volume (e.g. cd-roms)
# r            volume is read-only and always reports "0 byte free"
#              (this is intended for copies of CD-ROMs on harddisks)
# o            volume has only one filesystem/device/namespace
#              this is for filesystems with high inode > 0xFFFFFFF.
```

```
# because for namespace services mars_nwe normally use the
# first 4 bit of 32 bit inode for distinguish
# between several devices/namespaces for one volume.
# p 'PIPE' filesystem. All files are pipe commands.
# See 'doc/PIPE-FS'.
#
# O + OS/2 namespace.
# N + NFS namespace.
# .................................................
#
# Examples:
# 1 SYS /var/local/nwe/SYS k
# 1 HOME - k
# Use /var/netware for the SYS volume, and make it read-only
1 SYS /var/mars_nwe/sys rk
1 CDROM /mnt/cdrom kmr
# 1 SYS /u3/SYS/ k
```

Section 1 of the configuration file defines the SYS volume as a read-only volume that is located on the Linux server at /var/mars_nwe/sys and that allows lowercase characters in filenames. It also defines a volume CDROM, which is also read-only, allows lowercase filenames, and is marked as removable media. If you wanted to define a volume HOME that corresponded to the remote user's home directory on the Linux box, you could create an entry like the example shown in Listing 18.1 containing the word HOME.

Having completed the configuration of volumes in section 1 of the configuration file, we can now move on to section 2 (see Listing 18.2). In this section, we will configure the server name to be used by the NetWare emulator running under Linux.

### LISTING 18.2 Section 2 of the /etc/nwserv.conf File—Servername Configuration

```
# ===============================================================
# Section 2: servername (optional)
#
# The servername is the name under which this server will show up when
# using tools like "slist" (server-list).
#
# If you don't supply an entry for this section, the hostname of your
# Linux machine will be converted to all-uppercase and used as the servername.
#
# ---------------------------------------------------------------
# Syntax:
```
