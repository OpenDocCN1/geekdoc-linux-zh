# CHAPTER 11 Backing Up, Restoring, and Recovery

malicious programs.) Many modern laptops do not provide floppy drives except as an option.

Floppy drives are cheap and disposable solutions for making simple, quick backups of a few files by the user, but the media are easily damaged, lost, and accidentally overwritten. They also unexpectedly fail at times. Floppies now represent the low-rent district for data storage.

# Zip Drives

You can use removable or portable drives as part of your backup strategy. Of all the removable hard drive manufacturers, Iomega seems to have acquired some staying power with its Zip (100, 250, and 750MB). Although these drives have good support in Red Hat Linux, in the past they have been plagued with mechanical problems that have rendered drives retrievable. Their reliability has improved, but shy away from any older drives. These drives have been ubiquitous and common in the publishing industry. They are being supplanted by CD writers.

# USB and Solid-State Drives

USB hard drives and solid-state drives are the new kids on the block with prices dropping over the last year or two; a 32MB drive costs less than $50. The advantages using USB drives is their large capacity for their size. (Sandisks, also known as Compact Flash devices, are typically small, sizes up to 1GB if you are wealthy enough to afford them.) And both USB and solid-state drives are highly portable. Support for these drives under Red Hat Linux is very good, accommodating these drives by emulating them as SCSI drives. (The system sees them usually as /dev/sd1.) Watch for improved support and ever-falling prices in the future. The new USB 2.0 drives are significantly faster than the older USB 1.0 drives. A 100MB USB drive will cost about $150.

# Firewire Drives

Firewire (IEEE1394) drives are similar to USB drives, and they just use a different interface to your computer. Kernel support is available if you have this hardware; a 100GB Firewire drive will cost about $180, roughly twice IDE drives. Found mostly on the Mac, controller and drive hardware exist for the PC platform as well.

# CD-RW and DVD Drives

Compared to floppy drives and some removable drives, CD-RW drives and their cousins, DVD-R drives, can store large amounts of data and are useful for a home or small business. Once very expensive, CD burners and media are relatively inexpensive today, although automated CD changing machines, necessary for automatically backing up large amounts of data, are still quite costly. A benefit of CD and storage over tape devices is that the archived filesystem can be mounted and its files accessed just like a hard drive (you do when you create a CD, see Chapter 26, “Multimedia Applications”), making the recovery of individual files easier.