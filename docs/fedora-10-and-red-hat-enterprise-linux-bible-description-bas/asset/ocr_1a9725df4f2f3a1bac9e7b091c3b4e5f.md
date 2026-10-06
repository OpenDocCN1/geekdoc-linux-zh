On the Linux server, export a shared directory from the NFS facility as described in Chapter 18. To be able to use the shared directory from Mac OS X, however, you must be sure to add the insecure option. For example, share the /var/music directory from the Linux server named jukebox.linuxtoys.net, you can add the following line to the /etc/exports file on server:

```
/var/music    *(ro,insecure)
```

This example allows the /var/music directory to be shared with all computers (*) and provides read only permission. The insecure option allows clients that the exported directory make the request from an insecure port (ports above 1024). This is important because the Mac OS Connect to Server window makes its request to mount the shared directory from a port above 1024, and without the option.

On the Linux server, verify that the NFS service is running and re-export the shared directory by typing the following (as root):

```
# exports -a
```

On the Mac OS X client, Go to the Finder bar at the top of the screen, and select Connect to Server. The Connect to Server window appears.

On the Mac OS X client, type the address of the shared directory into the Address box. For example, connect to the shared nfs:// directory /var/music from the computer named jukebox.linuxtoys.net, you can type the address nfs://jukebox.linuxtoys.net/var/music (see Figure 26-5).

![](bbox=[0.239, 0.532, 0.814, 0.749])

Figure 26-5: Connect to an NFS server from the Connect to Server window.

If everything is working properly, an icon representing the server should appear on your Mac OS X desktop. Depending on which version of Mac OS X you are using, a window might just pop open, displaying the contents of the directory or you may need to open it to see the contents of the shared directory. You can use the shared files and directories as though they