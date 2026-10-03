# Using NFS on RHEL 9 to Share Files with Remote Systems

# 18.7 Accessing NFS Filesystems in Cockpit

In addition to mounting a remote NFS file system on a client using the command line, it is also possible to perform mount operations from within the Cockpit web interface. Assuming that Cockpit has been installed and configured on the client system, log into the Cockpit interface from within a web browser and select the Storage option from the left-hand navigation panel. If the Storage option is not listed, the *cockpit-storaged* package will need to be installed:

```
# dnf install cockpit-storaged
# systemctl restart cockpit.socket
```

Once the Cockpit service has restarted, log back into the Cockpit interface, at which point the Storage option should now be visible.

Once selected, the main storage page will include a section listing any currently mounted NFS file systems, as illustrated in Figure 18-1:

![](bbox=[0.135, 0.33, 0.81, 0.455])

Figure 18-1

To mount a remote filesystem, click on the ‘+’ button highlighted above and enter information about the remote NFS server and file system share together with the local mount point and any necessary options into the resulting dialog before clicking on the Add button:

![](bbox=[0.195, 0.555, 0.76, 0.75])

Figure 18-2

To modify, unmount or remove an NFS filesystem share, select the corresponding mount in the NFS Mounts list (Figure 18-1 above) to display the page shown in Figure 18-3 below: