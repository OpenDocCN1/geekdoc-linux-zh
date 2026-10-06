# CHAPTER 31 Backups 757

quickly, whereas data that rarely changes (such as the contents of the /etc directory) doesn't need to be backed up quite often. For these and other reasons, multiple backup policies might be needed to fit the types of data you are backing up.

When examining your requirements, take careful of compressible versus noncompressible data. With local disk capacities being so large, many individuals have taken to storing personal music/image/video collections on their work systems, and of course a lot of this data has nothing to do with the primary business functions. It is prudent to select your organization's policy on this issue so that expectations are met: If users think that all of the systems are backed up, they may be taken away when they find out their personal MP3 collection wasn't covered in that! On the flip side, you may be taken aback by a sudden increase in backup capacity requirements when users discover peer-to-peer (P2P) file sharing applications or bring their home MP3s to their computers at work.

# Hardware and Backup Medium

The type of hardware you choose should reflect the amount and type of data you need to back up, the frequency with which you're backing up, and whether it is necessary that backups get rotated to an offsite location.

The common choices available are tape, recordable CDs and DVDs, USB drives, cloud-based solutions, Storage Area Network (SAN), Network Attached Storage (NAS), and other networked storage arrays. Of these, tape has been around the longest and offers the widest available choices in media density, form, and mechanisms.

Among your choices for tape, selecting the specific type can be tricky. Many of the high-density options are appealing for the obvious reason that you can cram more data into a single tape. Of course, high-capacity tapes and drives typically cost more. Work toward finding an optimum solution that solves the most system data at the best price, with your requirements for media capacity.

> NOTE Many advertisements for tape drives boast impressive capacities, but keep in mind that these numbers are for the compressed data on tape, not the actual data. The amount of uncompressed data on tape is usually about half the compressed capacity. This is important to know, because compression algorithms achieve various levels of compression, depending on the type of data being compressed. For example, textual data compresses quite well, but certain graphics or video formats get little to no compression at all. When you estimate the amount of data you can store on a single unit, be sure to consider the mix of data on your servers.

![](bbox=[0.09, 0.625, 0.155, 0.665])

Disk-based backups are now a common phenomenon. The concept is simple: Back the contents of source drives A, B, and C to destination drives X, Y, and Z. The protocol or interface for communicating with the destination drives is another issue and if the primary goal of backups is to protect against simple accidents (file deletions going bad, and so on), this works well. Transfers are fast, media is cheap, and building a home-brew Redundant Array of Independent Disks (RAID) system using a low-cost PC, a decent RAID controller,

![](bbox=[0.09, 0.935, 0.155, 0.975])