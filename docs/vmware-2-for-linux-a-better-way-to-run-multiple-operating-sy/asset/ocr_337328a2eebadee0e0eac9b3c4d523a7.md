8. Now, mount the host drive on the guest at the location you just created. The command is of the form

```
mount <server IP>:<exported directory> /mnt/nfsm
```

The server IP is the address of the host. If you are running both bridged and host-only networking, use the one appropriate to the address range you specified in /etc/exports on the host.

The exported directory must match one of the entries in /etc/exports exactly (in this case, /home/jcompton).

To mount the drive I configured earlier, the command is

```
mount 192.168.20.2:/home/jcompton /mnt/nfsm
```

The output of this command appears in Figure B.7.

> Especially if you are using host-only networking, you can substitute the machine's name for the IP address, but it is faster to use the IP address. If you've forgotten, run /sbin/ifconfig on the host.

9. The drive is now mounted! You can cd to the mount point and open, copy, edit, and delete files as you see fit. When you are done, umount /mnt/nfsm (or whatever mount point you created in Step 7) to release the host file system from the guest.

![](bbox=[0.08, 0.88, 0.68, 0.97])

Figure B.7 It might look humble, but this VMware session is connected directly to my home directory over NFS.