data can threaten the user’s life. It’s designed to protect a user who has a gun to their head. Thankfully, that use case is rare; this book doesn’t cover it.

The geli(8) encryption system protects against more common risks. If your laptop is stolen, GELI prevents the thief from reading the hard drive.⁴ If you store your company’s financial records on a GELI-encrypted partition, the service tech can’t read it during a service call. Chapter 23 covers GELI in more detail.

Many organizations require disks containing financial data or intellectual property to be rendered unreadable when decommissioned. You can send such disks to be shredded, but encrypting the disks at install time is equally effective. The disks become unreadable when you destroy the encryption key.

I recommend encrypting either the entire system or none of the system. Partially encrypted disks leave opportunities for skilled intruders to sabotage your system and subvert the encryption.

Decide whether or not you need encryption before proceeding.

# Disk Partitioning Methods

Disk partitioning lets you divide a disk or disk array into logical units. Even hosts with average consumer-grade operating systems, such as the Windows laptop you’ll find at your local big-box store, ship with multiple partitions on the hard drive. A partitioning scheme is the system for organizing partitions on a disk.

Computing is always in transition between technologies, and right now we’re amidst a particularly annoying change in disk partitioning. Older and smaller hardware uses master boot record (MBR) partitioning and is always limited to disks of 2TB or smaller. Newer and larger hardware uses the more flexible and generally better GUID Partition Tables (GPT) scheme. FreeBSD manages both types of partition with gpart(8).

Which should you use in your install? Use GPT on any system that supports GPT, no matter the size of the disk. Use MBR if and only if the