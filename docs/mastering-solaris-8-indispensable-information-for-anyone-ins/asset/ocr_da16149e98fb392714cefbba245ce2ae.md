To share a home directory on a Solaris server, do the following:

+   1. Log in as the root on the system that will contain the user's home directory by entering the su command at the command line, if necessary.

+   2. Enter the share command to determine if the home directory has been shared. If the home directory isn't listed, you will need to set up a share point for that user's home directory.

+   3. Open the /etc/dfs/dfstab file and add the line share -F nfs /export/<home\_directory>.

+   4. At the command line, enter shareall -F nfs, then press the Return key. When you issue the shareall command, the /etc/dfs/dfstab file is run without your having to reboot the system. If you didn't issue the command, you would have to restart your system to have the shareall command run automatically.

+   5. Enter ps -ef | grep mountd and press the Return key to determine if the mountd daemon is running on your system. If the mountd daemon is running, the share is complete and established. Otherwise, perform step 6.

+   6. Enter /etc/init.d/nfs.server start and then press the Return key.

There are additional considerations that you need to account for after you share a home directory on a network. If you are running the NFSv4 or NIS server, enter the server's IP address and system name into the /etc/hosts file on the user's system. This can be done conveniently in the Hosts window of the AdminTool program. You might also want to create disk quotas for a user at this point to limit the size of their home directory on a server. To make the home directory available, you must add it to the Auto\_home database so that AutoFS will mount it automatically (preferred in a network environment), or you can add the entry to the /etc/vfstab file so that the NFS service can mount the directory. The procedure for mounting a newly established home directory using the NFS service is very similar to procedure just described. Follow these steps to have NFS mount a home directory:

+   1. As a superuser, add the entry for the user's home directory into the /etc/vfstab file; the entry will be similar to the following:

```
`<systemname>:/export/home/<username> \home/<username> nfs \- yes, rw, intr`
```

+   2. Then create the mount point with the mkdir /home/<username> command.

+   3. Use the chown command to assign the directory ownership to the user account.