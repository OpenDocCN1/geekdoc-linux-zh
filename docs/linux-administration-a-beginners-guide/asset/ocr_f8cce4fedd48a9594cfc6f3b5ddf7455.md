# Remote Printer Access

So the head of marketing got a brand-new color laser printer, but your request for a wrist brace to help with your carpal tunnel was turned down. It’s only fair that you get to use the printer, right!

If that printer is sitting on an NT server that doesn’t have Lpd configured, but it does share the printer via SMB so other Windows workstations can print to it, you’re in luck. You can use `smbs1ent` to submit print jobs to other NT or Samba servers just as a Windows client would.

To connect to a printer on a server using **smbs1ient**, use the `-r` parameter and specify the service name for the printer, as shown here:

```
``` 
[root@ford root]# smbs1ient //ford/lp -p 
```
```

This connects you to the service as a printer. You can then issue the print command along with the name of a local filename. For example, if I have a file called *bleeker* in the directory I run **smbs1ient** from, I can issue this command:

```
``` 
smbs1-> print bleeker 
```
```

to print the contents of the file *bleeker*.

Possible uses for this remote printer access feature includes setting up special filters in /etc/printcap files so that all files printed to a particular printer are automatically redirected to a Windows printer on the network. (See Chapter 21.)

# USING SMBMOUNT

If your kernel is configured to support the SMB file system (as are most kernels that come with Linux distributions), you can actually mount an NT or Samba share onto your system in much the same way you would mount an NFS partition. This is very handy for accessing a large disk on a remote server without having to shufle individual files across the network.

To use **smbmount**, simply run this command:

```
``` 
[root@ford /mnt]# smbmount //ford/sahash /mnt/sahash 
```
```

where //ford/sahash is the share being mounted and /mnt/sahash is the directory to which it is being mounted. To unmount this directory, run umount:

```
``` 
[root@ford /mnt]# umount /mnt/sahash 
```
```

# ENCRYPTED PASSWORD SUPPORT

Because Windows uses a password hashing algorithm different from Linux’s, Samba needs to maintain its own password file in order to support encrypted password support.