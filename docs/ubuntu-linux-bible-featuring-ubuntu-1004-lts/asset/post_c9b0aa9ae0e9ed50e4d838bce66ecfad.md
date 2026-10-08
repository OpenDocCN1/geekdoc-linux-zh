
and directory protection using Users and Groups on Ubuntu systems, and then discussed how users perform tasks that require system privileges on Ubuntu systems using the sudo command.
The last section of the chapter explained how to install and configure Kerberos authentication on your system to provide a centralized, network-oriented authentication mechanism.

The next chapter discusses how to back up and restore files on Ubuntu systems in a variety of local and network-oriented mechanisms. Backups are probably the definitive mundane system administration task, even when automated. However, should your hard drive crash or you accidentally delete your thesis, the genealogical research you've been working on for a decade, all of your e-mail, or your entire music collection, your backups will quickly become your best and most loyal friend.

## Backing Up and Restoring Files

Backups are spare copies of the files and directories that are found on a computer system, written to and stored on removable media that is preferably stored other than on your computer. Doing backups are time-consuming, but absolutely mandatory, task if you place any value at all on the files, e-mail, and other data that you have stored on your computer.

Backups are exactly like auto insurance policies—well, almost exactly, because they're not a legal requirement to own a computer system (in most states). You need them, and you hope that you never do. They are usually all just time-consuming and expensive (your time has some value, right?). However, one rainy night when you discover that you've accidentally deleted your home directory or when a user comes to you and says that they've accidentally deleted your company's personnel records, or the source code for your company's products, you'd better have a good answer. The right answer, of course, is "I'll restore that from backups immediately."

It's hard to think of anything that so thoroughly combines the mundane and mandatory as backing up your data. It's boring. And, of course, it's critical. This chapter is oriented toward you as a systems administrator, regardless of how many systems you're responsible for. As system administrators, our responsibility is to provide secure, well-maintained, and rigorously backed-up systems. It is important to understand that backups are not just for when things go wrong, but also for peace of mind. If a drive fails, or a user accidentally deletes a file, or a natural disaster occurs, your backups are your only line of defense.

The following list outlines the types of backup strategies we will cover in this chapter:

- Backups to local media
- Backups to remote storage
- Using rsync for backups
- Using time machines (for macOS users)
- Backing up to the Cloud

## Part III: Ubuntu for System Administrators

This chapter explains a variety of solutions for creating backups, ranging from command-line tools to graphical interfaces. Before discussing the tools, it's useful to review some basic concepts. Although you may already be familiar with these, they are important to ensure we are all on the same page before we dive into the technical details.

## Why Do Backups?

Another alternative using physical devices for backups is to back up your data to one of the many cloud-based backup solutions that are available today, including Ubuntu's own Ubuntu One. These are perfectly suited for backing up critical files and directories, liberate you from having to provide your own backup media, inherently deliver the benefits of off-site storage. In my opinion, cloud-based backup solutions are less suitable for academic or enterprise backups for reasons including security and the difficulty of time required for doing complete system restores (AKA "bare-metal" restores) from remote storage that require network access.

## Backing Up and Restoring Files

The following list outlines the types of backup strategies we will cover in this chapter:

- Backups to local media
- Backups to remote storage
- Using rsync for backups
- Using time machines (for macOS users)
- Backing up to the Cloud

## A Few Words about Backup Media

Backups take a significant amount of time and require a significant investment in media. Nowadays, home systems store tens of gigabytes, which means you either need high-capacity backup devices, or you must prepare for a laborious day or two of loading CDs or DVDs.

USB sticks (AKA "thumb drives") are eminently suitable for backing up individual files because they are inexpensive and typically provide enough storage for most users. For us, I personally prefer CD-R and DVD-R over their rewritable brethren because of the cost difference and that rewritable CDs and DVDs are only good for a limited number of uses. On the other hand, CD-R and DVD-RS are relatively appropriate for enterprise backups because even DVD-RS are not large enough to back up complete systems; it's tricky to split backups across DVD-R media, and DVD-RS are relatively slow to write. They can be useful when restoring a system because of their portability—you can take them directly to the system you're restoring without having to make a tape drive, do a network restore, and so on. I personally prefer hard drives in enterprise or academic environments.
