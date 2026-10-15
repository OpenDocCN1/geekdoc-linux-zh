
# LPIC1 LINUX ADMINISTRATOR--EXAM 101

- `sudo apt -y install xfsprogs`
- `sudo mksfs.xfs [dev]p2`
- `mkdir lab57-ext4 lab57-xfs`
- `sudo mount [dev]p1 lab57-ext4`
- `sudo mount [dev]p2 lab57-xfs`
- `sudo dd if=/dev/urandom of=lab57-ext4/random bs=1M count=500`
- `sudo dd if=/dev/urandom of=lab57-xfs/random bs=1M count=500`
- `md5sum lab57-{ext4,xfs}/random`

What you've just done is created two filesystems on your block device and filled them up with a file containing random data. Then you obtained the `md5` hash of each file, which you should save for later.

## Task 2

Now, you get to do something you would never do on a live system... cause damage, intentionally!

- `sudo umount [dev]p1 [dev]p2`
- `sudo dd if=/dev/urandom bs=1 count=10M of=[dev]p1 seek=1M`
- `sudo dd if=/dev/urandom bs=1 count=10M of=[dev]p2 seek=1M`

You've just caused some significant corruption to both filesystems, though unfortunately because of the nature of such corruption, the results can't be predicted. What you should do is attempt to remount both filesystems and get the `MD5` sums again:

- `sudo mount [dev]p1 lab57-ext4`
- `sudo mount [dev]p2 lab57-xfs`
- `md5sum lab57-{ext4,xfs}/random`

However, it's possible that `md5sum` or even `mount` will fail for one or both filesystems. Make sure the filesystems are unmounted again, then run:

- `sudo fsck [dev]p1`
- `sudo xfs_repair [dev]p2`

You should then be able to mount the filesystems again. However, you may notice that the `MD5` sums of your "important" data have been permanently altered. This is the unfortunate fact of filesystem corruption--not everything can always be saved.
