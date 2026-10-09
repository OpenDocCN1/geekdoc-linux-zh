As a demonstration, we'll try to mount a floppy disk using the mount command and later unmount it to understand how the process of mounting and unmounting drives works (you'll need a floppy disk for this).

We start out by trying to list the `/mnt/floppy` directory. No files are listed since the floppy drive device has not yet been mounted to `/mnt/floppy`:

```
```
$ ls /mnt/floppy/         before mounting the floppy drive
no files listed
```
```

We attempt to mount floppy drive device `/dev/fd0` to `/mnt/floppy`. However, we are prevented from doing so since this is a privileged operation allowed only for administrators or programs that have the setuid bit set. So we switch to the root user and try to mount the drive. This time we succeed in mounting the `/dev/fd0` device to `/mnt/floppy`:

```
```
$ mount /dev/fd0 /mnt/floppy
mount: only root can do that
$ su
Password:
# mount /dev/fd0 /mnt/floppy
# df -k|grep floppy
/dev/fd0                   1423    105    1318   8% /mnt/floppy
```
```

The `mount` command minimally takes two arguments. The first is the name of the device containing a file system to mount, and the second is a directory to map the device on to. We verify this using the `df` command whose output is piped to the `grep` command which searches for the string 'floppy' and sure enough, the drive is listed as being mounted to `/mnt/floppy`.

Once this is done, non-root users may also access the `/mnt/floppy` directory. We can exit from the root shell and assume our previous identity of a regular user:

```
```
# exit
$ ls /mnt/floppy/
aliases.txt  df.txt       ff.html    ps_A.txt     testcmd.sh   which.txt
crontab.txt  env.txt      parted.txt ps_auxww.txt top.jpeg
```
```

Now, as a normal user, we can list the files under the `/mnt/floppy` directory:

```
```
$ umount /dev/fd0
umount: only root can unmount /dev/fd0 from /mnt/floppy
$ su
Password:
# umount /dev/fd0
# exit
exit
$ ls /mnt/floppy/
bash$
```
```