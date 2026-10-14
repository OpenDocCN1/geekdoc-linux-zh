Most of the arguments here are pretty self-explanatory. The `--create` option tells `mdadm` that I want to create a new MD device at `/dev/md0`. If I already had a RAID array at `/dev/md0`, I would just pick the next number, such as `/dev/md1`. The `--level` option sets which RAID level to use for this array, `--raid-devices` sets the number of active devices, and finally you specify each partition you want to use for the array.

In my case I want to set up a RAID 5 array across `/dev/sdb1`, `/dev/sdc1`, and `/dev/sdd1`, so I would type

```
```bash
$ sudo mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb1
  /dev/sdc1 /dev/sdd1
mdadm: array /dev/md0 started.
```
```

Once I have created the array, I can check out its current health in the `/proc/mdstat` file:

```
```text
$ cat /proc/mdstat
Personalities : [raid6] [raid5] [raid4]
md0 : active raid5 sdd1[2] sdc1[1] sdb1[0]
      16771584 blocks level 5, 64k chunk, algorithm 2 [3/3] [UUU]

unused devices: <none>
```
```

Now I can treat `/dev/md0` like any other partition and format it with a file system of my choice and then mount it:

```
```bash
$ sudo mkfs -t ext3 /dev/md0
$ sudo mkdir /mnt/storage
$ sudo mount /dev/md0 /mnt/storage
```
```

Now this array is up and functioning; however, it is not yet set up to automatically start and mount at boot time. If you don’t set this up, you will have to run an `mdadm` command to assemble the array along with a `mount` command each time the system boots. To start the array at boot time, you need to configure `/etc/mdadm/mdadm.conf` with details about your array. Now you could certainly do this by hand, but `mdadm` provides a simpler way. The `mdadm --detail --scan` command will output an `mdadm.conf`