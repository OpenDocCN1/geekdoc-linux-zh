To make sure you're running the needed utilities, you can run the startup scripts with the status option. Here's how to do this:

+   Switch to the directory where network scripts are stored. On Red Hat and kindred systems, this directory is /etc/rc.d/init.d.
+   Type .portmap status and press Enter. You should see a message stating that portmap is running. If not, type .portmap startup and press Enter.
+   Now, type .nfs status and press Enter. You should see a message informing you that rpc.mountd and nfsd are running. If not, type .nfs start and press Enter.
+   Type /usr/sbin/pcinfo -p and press Enter. You should see a list of all the running daemons, including their version numbers and the protocol they're using.

If you see an error message such as “Can't contact portmapper” or “Connection refused,” or “Prog not registered,” portmap isn't running, or your /etc/hosts.deny and /etc/hosts.allow files aren't properly configured. Check your configuration, then restart your system and try the previous steps again.

# ## Configuring /etc/exports

The next step involves modifying the file /etc/exports on the server so that NFS knows which directories to “export,” that is, make available to clients. To specify a directory to export, type the name of the directory you want to export, followed by a space, and the IP address of the client or clients to which you want to make the directory available. After the IP address, place the export options you want within parentheses. Here's an example:

```
```
/home/suzanne 192.168.100.33(rw)
/mnt/cdrom 192.168.100.*(ro)
```
```

This example exports /home/suzanne, a directory owned by the user named suzanne on the server, to Suzanne's computer (192.168.100.33), where it will be available to her through NFS. The option (rw) specifies that this directory should be exported with read and write permissions