Snapshots are stored in Amazon S3 and take on all the desirable attributes that you'd expect. In particular, they're stored at low cost with high reliability.

The snapshot's state will eventually transition to "completed." The volume has been backed up:

```
```
$ ec2-describe-snapshots
SNAPSHOT     snap-c7e849ae   vol-73d4211a   completed
             2009-08-20T19:52:35+0000      100%
```
```

EBS snapshots can be used to create new volumes in the same or different availability zone. This is achieved by including the snapshot ID (snap-c7e849ae in my example) when the volume is created. I can create a new volume, with contents identical to the original at the time that I created the snapshot, as follows:

```
```
$ ec2-create-volume -z us-east-1b -s 50 --snapshot
  snap-c7e849ae
VOLUME      vol-00d72269   50   snap-c7e849ae   us-east-1b
             creating    2009-08-20T20:17:35+0000
```
```

Once the new volume's state turns to **available**, I need to attach it to an instance (in this case I'll use the same one that I started with, but they can be attached to any EC2 instance in the same Availability Zone), create a mount point, and then mount it, all in one fell swoop this time:

```
```
$ ec2-attach-volume vol-00d72269 -i i-da8f6db2 -d /dev/sdg
ATTACHMENT  vol-00d72269   i-da8f6db2   /dev/sdg
             attaching   2009-08-20T20:21:18+0000
```
```

Next, create a mount point:

```
```
<dev>: mkdir /data2
<dev>: mount /dev/sdf /data2
```
```

At this point /data and **data2** are exact duplicates of each other.

I can add more data to /data and then create another snapshot:

```
```
<dev>: cp -r /usr/java /data
```
```