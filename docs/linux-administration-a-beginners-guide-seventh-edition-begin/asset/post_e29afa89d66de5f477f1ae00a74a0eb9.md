
a few commodity disks can be done for relatively little money. More expensive commercial solutions, such as those from NetApp, offer more high-capacity options for larger installations with additional features.

> TIP: If you don't mind getting your hands dirty and a very minimal learning curve, you should seriously consider using the free alternatives to the packaged commercial storage appliances. Several free and open source solutions are available. One incredibly solid and mature example is the FreeNAS project (www.fennas.org).

Using disk-based backups, scheduled file copies can be automated with no tape swapping, and additional capacity can be added cheaply. The downside to this method is that off storage is not so easy. While getting hot-swappable hard disks is possible, they are not as robust as tape when it comes to being handled and moved. For instance, a tape can be dropped several times with no risk, but the same cannot be said of dropping a hard disk.

With record CDs and recordable DVDs, low-cost backups have become a real possibility. These optical media are easy to use and are the cheapest options. Unfortunately, they also hold less than their disk counterparts and have qualitative lifetimes. If the amount of data that needs to be backed up is not too large or the data does not change once backed (such as images), this type of media works well. For the purpose of backups, the media lifetimes vary by vendor. It is reasonable to expect a few years from optical media.

A combination between fixed and removable media is also increasing in popularity. In combination solutions, regular backups are made to disk, with periodic backups moved from the backup disk to tape.

In all of these backup options, you should always plan for possible media failure—that is, plan to make backed-up data new every few years. This is necessary to ensure that you're not just using new media, but the drive itself is still calibrated and modern equipment can still read and write it. In some cases, you might need to consider the data format. After all, data that can be read but not understood doesn't do anyone good! A good case in point is, for example, whether you can still make use of the contents of a 3.5-inch floppy disk from 25 years ago!

# Network Throughput

Unfortunately, network throughput is easily forgotten in the planning of backup operations. A really fast server and storage subsystem isn't very efficient if you feed the data through a thin straw!

Take the necessary time to understand your network infrastructure. Look at where the data is coming from and where it's going. Use Simple Network Management Protocol (SNMP) tools, as MRTG (www.mrt.org), to collect statistics about your routers and switches. In the off-chance that you need to back up machines that are connected via hubs, a backup sequence that won't back up two machines at the same collision domain at the same time. Overall, setting up and having a virtual area network (VLAN) dedicated to backups or other data transfers is a great idea.

# CHAPTER 31 Backups

Gathering all this information will help you estimate the bandwidth necessary to perform backups. With your analysis done, you'll be able to figure out which new gear or improvements will net you the best return for your money.

# Speed and Ease of Data Recovery

When requests to restore data arrive, you're likely to be under the gun to get the data back to the user(s) as quickly as possible. How long your users have to wait will depend on the tool used for backup. This means you need to incorporate the cost of response time into your backup evaluation. How much are you willing to spend to get the response time you need for a restore?

Disk-based restores are, of course, the fastest. They also offer the possibility of online backups, where users can visit the backup server themselves and copy the file. Recordable CDs and DVDs are quick, since the file can be quickly pulled from disk and given to the user as tape. By comparison, it is much slower. The specific file/data on the tape needs to be found, the archive read, and an individual file extracted. Depending on the speed of the tape and the location of the file, this can take a little bit of time.

So remember to factor the speed and ease of data recovery into the equation when choosing your backup solution, because there isn't much point in having a high-end and extensive backup solution when the backed-up data is not available to the people who need it.

# Data Deduplication

Besides being a bit of a mouthful to say, data deduplication deals with reducing redundant data in a storage system. It's another way of saying “data un-copying.”

We will use the scenario below to explain how deduplication works. Let's pretend that there are two users who both need to back up the same 10GB file. User A backs up the file to the backup server. Later, User B backs up the same file. Without deduplication, the backup server would use 20GB of space. With deduplication, the server recognizes that the file is already there and only stores a pointer for User B's copy of the file. This saves 10GB of space.

# Tape Management

As the size of your backups grows, so will you need to manage the data you backup. This is where commercial tools often come into play. When evaluating your choices, be sure to consider their indexing and tape management. It does you no good to have 50 tapes' worth of data if you cannot find the right file.

# Tape Performance Considerations

When you look at tape-based backups, consider where the tape drive itself will be kept and what system it will be connected. Will the tape be on a busy server already having a lot of active disks? Will it be kept on a dedicated server with disks? Is there any contention on the bus used to transfer data to it? For example, if you're backing up to a SCSI attached tape drive, you'll need to factor in the effect of the other devices on the same SCSI chain.

Finally, are you able to feed the tape drive fast enough so that it can stream? If the tape cannot stream, it will stop writing until it gets more data. This pause can be seconds long on a slow mechanism, while the drive realigns itself with the tape and finds the next available position to write data. Even if the pause is brief, when it occurs thousands of times during a single backup, it can increase your backup runtimes by many hours.
