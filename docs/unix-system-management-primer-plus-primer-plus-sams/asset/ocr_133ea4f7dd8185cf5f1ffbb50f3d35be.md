# UNIX SYSTEM MANAGEMENT PRIMER PLUS

learned this in Chapter 9, "Preparing for Disaster Recovery." When such failures occur, you can direct all traffic to your backup site through various means, including static routing and red-dressing in DNS.

But hardware is only part of location redundancy; you must have a copy of your data at the other site. The traditional way to accomplish this is by restoring from backup tapes, but this technique presents the following three problems:

+   - Transporting the tapes to the hot site takes.
- Restoring the tapes might take hours.
- The restored data is not current—it is probably missing data that changed just a few hours before the restore.

These are probably acceptable risks to most organizations. But for those organizations, who have a lower tolerance for downtime and data loss, such as banks and insurance companies, the following sections will discuss alternative methods of replicating data to alternative sites and how to provide access to the data at those sites.

# Remote Mirroring

Remote mirroring solves the problem of long tape backup, time-consuming restore, and stale backup at the hot site. Remote mirroring typically involves using one storage device to propagate incremental changes in its data in real time (or near real time) to a second storage device in a remote location. Sending only incremental changes over the network ensures that this solution will work with limited bandwidth, such as that of a T1.

Initially, you must seed the secondary device with a full copy of your data, but all subsequent updates will be incremental. Several hardware and software products can provide this functionality:

+   - SnapMirror from Network Appliance
- Symmetricrix Remote Data Facility (SRDF) from EMC
- HP MirrorDisk/UX
- Oracle Advanced Replication

Remote mirroring can be an expensive alternative to tape restores. But the time you save by not having to perform a restore and the ability to transfer data with no loss of currency may justify the cost.

# Content Distribution

One of the most popular applications on the Internet today is multimedia. News and sports sites use audio and video clips extensively, and those sites must potentially be available to millions of clients at one time. Multimedia transfers, with pictures, movie, and audio clips, can consume megabytes and gigabytes of bandwidth; very companies have the resources