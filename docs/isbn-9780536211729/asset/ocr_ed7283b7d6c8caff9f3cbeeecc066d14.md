+   4. Update the usage message by finding the line containing

[-p server-password]

and changing that portion to

[-P server-password-file]

+   5. Being perfectionists, change the line

```
/* clean up the command line in case -p was used */
```

to

```
/* clean up the command line in case -P was used */
```

+   6. Search for -p in popclient.il, the man page, and make the obvious changes to document-P.

+   7. Compile it via make and install (running as root) via make install.

# 3.8 Doing the Samba

| DANGER LEVEL |

Samba is a network service that allows Windows clients to communicate with a Linux server using a protocol called CIFS. CIFS stands for Common Internet File Service.

> This section on Samba generously was written exclusively for this book by Larry Gee, an experienced Samba administrator. He has revised it extensively for this edition.

In an earlier life, CIFS was called SMB, which stands for Server Message Block, the name SamBaMB. According to the Samba team, Microsoft’s published SMB/CIFS specification was not correct and the Samba team had to reverse the actual protocol by sniffing the network during SMB operations between Windows clients and servers. (I had a similar experience with Sun’s NFS specification when I created an NFS server for a non-UNIX operating system from scratch.)