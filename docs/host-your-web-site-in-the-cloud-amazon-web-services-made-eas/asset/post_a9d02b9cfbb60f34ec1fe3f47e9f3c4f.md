
arbitrary, by convention they reside in the /dev directory and have names that start with sd, followed by another letter. The EC2 system disk is /dev/sda and the other local disks (on the larger-sized instances) are sdb, sdc, and so forth. /dev/sdf is a good device name for the first EBS volume attached to the instance (as “f” is far enough down the alphabet to avoid colliding with another device). Here’s how to attach it:

```
$ ec2-attach-volume vol-73d4211a -i i-da8f6db2 -d /dev/sdf
ATTACHMENT vol-73d4211a i-da8f6db2 /dev/sdf
attaching 2009-08-20T19:26:08+0000
```

The command accepts the volume ID, followed by -i and the instance ID, and -d and the device name. The volume status changes to “attaching.” It will stay in this state for a few seconds before transitioning to “attached”:

```
$ ec2-describe-volumes vol-73d4211a
ATTACHMENT vol-73d4211a i-da8f6db2 /dev/sdf
attached 2009-08-20T19:26:12+0000
```

At this point, we have done the cloud computing equivalent of procuring a disk drive, plugging it into a server, and attaching the data cable. The disk is physically connected and running; the operating system is aware of it, but the disk is raw (unformatted) and yet to be part of the file system.

The next step is to create a file system on the new volume and an attachment (mount point), and we can logically mount the volume on the instance’s root file system. We’ll follow the same procedure from the section called “Creating an EBS Volume” in Chapter 5 (you’ll need to log in to your EC2 instance to run these commands):

```
<dev>: mkfs -F /dev/sdf
<dev>: mkdir /data
<dev>: mount /dev/sdf /data
```

You can mount an EBS volume on any location in your instance’s file system. If you’re planning to create and use a large number of volumes, you should take the time to plan out a logical name structure beforehand.

The volume is now ready for use. You can create directories, store files, and do whatever you need to inside of the /data directory hierarchy. I’m going to need some data in my /data directory for the examples in the next section, so I’m going to copy the contents of /usr/lib (about 250MB) over:

```
<dev>: cp -r /usr/lib /data
```

# EBS Snapshots

Let’s say that I want to create a backup of my EBS volume as it exists at this point. The first step is to make sure that any in-memory data has been written to disk:

```
<dev>: sync
```

If you’re using the EBS volume to store database files, you should probably shut the database server down before you create the backup. This will ensure that the backup is complete and logically consistent.

Creating the backup—a snapshot in EBS terms—is very easy:

```
$ ec2-create-snapshot vol-73d4211a
SNAPSHOT snap-c7e849ae vol-73d4211a pending
2009-08-20T19:52:35+0000
```

Once the snapshot has been initiated, it’s safe to resume writing data to the volume. The snapshot may take some time to complete, but it will always represent the state of the volume at the time the snapshot was initiated.

You can check on the status of your snapshot like this:

```
$ ec2-describe-snapshots
SNAPSHOT snap-c7e849ae vol-73d4211a pending
2009-08-20T19:52:35+0000
```

The first snapshot for an EBS volume is similar to a traditional, full backup. It contains all the information written to the volume. Second and subsequent snapshots are similar to traditional incremental backups. They contain only the information that’s been changed since the previous backup. EBS takes care of all the details of this behind the scenes. Even if you delete the first snapshot, sufficient data will be retained to allow you to create new volumes from any of the other snapshots.

Snapshots are stored in Amazon S3 and take on all the desirable attributes that you'd expect. In particular, they're stored at low cost with high reliability.

The snapshot's state will eventually transition to "completed." The volume has been backed up:

```
$ ec2-describe-snapshots
SNAPSHOT     snap-c7e849ae   vol-73d4211a   completed
             2009-08-20T19:52:35+0000      100%
```

EBS snapshots can be used to create new volumes in the same or different availability zone. This is achieved by including the snapshot ID (snap-c7e849ae in my example) when the volume is created. I can create a new volume, with contents identical to the original at the time that I created the snapshot, as follows:

```
$ ec2-create-volume -z us-east-1b -s 50 --snapshot snap-c7e849ae
VOLUME      vol-00d72269   50   snap-c7e849ae   us-east-1b
             creating    2009-08-20T20:17:35+0000
```

Once the new volume's state turns to available, I need to attach it to an instance (in this case I'll use the same one that I started with, but they can be attached to any EC2 instance in the same Availability Zone), create a mount point, and then mount it, all in one fell swoop this time:

```
$ ec2-attach-volume vol-00d72269 -i i-da8f6db2 -d /dev/sdg
ATTACHMENT  vol-00d72269   i-da8f6db2   /dev/sdg
             attaching   2009-08-20T20:21:18+0000
```

Next, create a mount point:

```
<dev>: mkdir /data2
<dev>: mount /dev/sdg /data2
```

At this point /data and /data2 are exact duplicates of each other.

I can add more data to /data and then create another snapshot:

```
<dev>: cp -r /usr/java /data
```

```
$ ec2-create-snapshot vol-73d4211a
SNAPSHOT       snap-b1ed4cd8 vol-73d4211a pending
2009-08-20T20:27:04+0000
```

I now have two snapshots (with different contents) of the same volume. I can create new volumes from either one:

```
$ ec2-describe-snapshots
SNAPSHOT       snap-c7e849ae  vol-73d4211a  completed
2009-08-20T19:52:35+0000     100%
SNAPSHOT       snap-b1ed4cd8  vol-73d4211a  completed
2009-08-20T20:27:04+0000     100%
```

On a production system you’ll probably have lots and lots of snapshots. Take care to track the reason for each snapshot (for example, “Snapshot of development volume on Mac’s instance before beta release 1.5”). You could write this on a sticky note and keep it under your keyboard, or you could write a little AWS program to capture the data in SimpleDB.

In fact, we can combine the snapshot and the logging. We will need a SimpleDB domain:

```php
# chapter_10/include/book.inc.php (excerpt)
define( 'BOOK_SNAP_LOG_DOMAIN', 'snapshot_log');
```

Make sure you create this SimpleDB domain before you run the next script. You can use the `create_domain.php` script again. Here’s all it takes:

```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

if ($argc < 3)
{
    exit("Usage: " . $argv[0] . " \"message\" VOLUMEID...\n");
}

$message = $argv[1];

$sdb = new AmazonSDB();
$ec2 = new AmazonEC2();

for ($i = 2; $i < $argc; $i++)
{
    $volId = $argv[$i];

    // Create snapshot
    $res1 = $ec2->create_snapshot($volId);

    if ($res1->isOk())
    {
        $snapId     = $res1->body->snapshotId;
        $startTime = $res1->body->startTime;

        $key = $volId . '_' . $startTime;

        $attrs = array('VolId' => $volId,
                       'Message' => $message,
                       'StartTime' => $startTime);

        $res2 = $sdb->put_attributes(BOOK_SNAP_LOG_DOMAIN, $key,
                                $attrs, true);
    }
}
exit(0);
?>
```

The create_snapshot method initiates the snapshotting activity on the specified volume. The snapshot ID and the start time are extracted from the data that it returns, and the information is stored in SimpleDB.

Running the script is easy:

```
$ php snap_and_log.php "Important Backup" vol-73d4211a
```

Just to be clear, this tiny program creates a near-instantaneous backup of a volume that can be up to one terabyte in size, stores the backup in Amazon S3 for safekeeping, and logs the salient information to SimpleDB. That’s cloud computing (and the power of complete programmability) in action!

The EBS snapshots are stored in S3, so it’s impossible to reach them using the S3 APIs. You can access them through the `ec2-describe-snapshots` command or you can write a program to call CloudFusion’s `describe_volumes` method.

## EBS Public Data Sets

You can also create EBS volumes from the EBS Public Data Sets. The data sets (listed at http://aws.amazon.com/publicdatasets/) contain public information for use with AWS. There’s census data, genome data, economic data, and much more. Each data set is provided in the form of an EBS snapshot. Instead of spending hours or even days downloading and unpacking this data (some of the data sets contain hundreds of gigabytes of information), you can simply create a volume and start processing the data right away.

For example, the Wikipedia Page Traffic Statistics data set contains 320 gigabytes of hourly page statistics for the popular Wikipedia site.[1] Here’s how to use it:

```
$ ec2-create-volume -z us-east-1b --snapshot snap-753dfc1c
VOLUME vol-42d1242b 320 snap-753dfc1c us-east-1b
creating 2009-08-20T21:19:26+0000
$ ec2-attach-volume vol-42d1242b -i i-da8f6db2 -d /dev/sdh
ATTACHMENT vol-42d1242b i-da8f6db2 /dev/sdh
attaching 2009-08-20T21:20:08+0000
```

```
<dev>:\> mkdir /wikipedia
<dev>:\> mount /dev/sdh /wikipedia
```

The data was available to me—in directory /wikipedia—in 20 seconds (quite literally, as fast as I could type).

A volume of this size will cost about $30 per month, so be sure to `umount`, detach, and destroy it when you no longer need it. Here’s all it takes:

```
<dev>:\> umount /dev/sdh
<dev>:\> mount /dev/sdh /wikipedia
```

1. http://www.wikipedia.org
