# LISTING 18.1 continued

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

Section 1 of the configuration file defines the SYS volume as a read-only volume that is located on the Linux server at /var/mars_new/sys and that allows lowercase characters in filenames. It also defines a volume CDROM, which is also read-only, allows lowercase filenames, and is marked as removable media. If you wanted to define a volume HOME that corresponded to the remote user's home directory on the Linux box, you could create an entry like the example shown in Listing 18.1 containing the word HOME.

Having completed the configuration of volumes in section 1 of the configuration file, we can now move on to section 2 (see Listing 18.2). In this section, we will configure the server name to be used by the NetWare emulator running under Linux.

# LISTING 18.2 Section 2 of the /etc/nwserv.conf File—Servername Configuration

```
# ===============================================================
# Section 2: servername (optional)
#
# The servername is the name under which this server will show up when
# using tools like "slst" (server-list).
#
# If you don't supply an entry for this section, the hostname of your
# Linux machine will be converted to all-uppercase and used as the servername.
#
# ---------------------------------------------------------------
# Syntax:
```