information until the server responds. This is important, for if you mount filesystems with the soft option, you risk the potential for application or system failure if the client “gives up” asking for data if the NFS server is busy, down, or if you have network failures.

bg—This background option is most useful when incorporated into your fstab/vfstab file to be used at boot time. The background option instructs the mount command to run in the background, and continue running until the mount is successful. In the event of NFS server problems or network slowness, the mount command running in the background will allow your system to continue booting instead of waiting for the mount command to complete. The fstab/vfstab file will be discussed in more detail in the next section.

> A good rule of thumb is to always use the hard and bg options.

For example, machine mars has a filesystem, /users/data, that it wants to share with machine earth. On earth, we want the information in directory /users/data to be visible to users on earth in /remote/data. The command should take the form:

```
earth# mount mars:/users/data /remote/data
```

As another example, on earth we have a local CD drive that resides in the directory /devices/cdrom and that we want to mount read-only into the directory /local/cd. The command looks like:

```
earth# mount -o ro /devices/cdrom /local/cd
```

The mount command is a simple, useful command for both attaching local data as well as sharing remote data. You may now ask the following question: What if I want to remove the mount filesystem? For once we have a simple and intuitive answer—use the umount command. The umount command unmounts the mounted filesystem when used in the form: umount <filesystem>

Be careful not to unmount filesystems that are in use by users or the system.

In Figure 8.1, we have the home directory /users/data/sjflynn on the NFS server saturn, mounted on the local system mars, in /home/sjflynn. Note that an attempt to unmount the filesystem failed, most likely because the user sjflynn still had an active shell with /home/sjflynn as part of the current path.