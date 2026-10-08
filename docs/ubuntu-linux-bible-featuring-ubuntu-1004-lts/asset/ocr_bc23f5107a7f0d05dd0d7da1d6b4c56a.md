# Part III: Ubuntu for System Administrators

This chapter explains a variety of solutions for creating backups on Ubuntu Linux systems, ranging from command-line solutions to some impressive graphical tools. It also covers the flip side of making backups — restoring files from them — which is what makes backups worthwhile in the first place.

# Backups 101

Before discussing the tools used to create backups, it's useful to review some of the basic issues and approaches in backing up any kind of computer system. Although you may already be familiar with these concepts and occasionally bumble backup and restore commands in your sleep, providing a clear picture of what you're trying to accomplish in backups and how backup systems are usually designed provides a firm foundation for discussing the various tools discussed later in this. Since I have no way of knowing whether you're reading this book because you're using Ubuntu on your home computer or because you're deploying Ubuntu throughout your work, I'm going to err on the side of caution and discuss many topics that are overkill for a home computing environment but are mandatory in multi-system business or academic environments.

# Why Do Backups?

In an ideal world, backups would not be necessary. Computer hardware and software would always work correctly, users would never make mistakes, and I'd be a rock star. Unfortunately, in the real world, things are different. Computer system administrators and other members of an MIS/IT department manage backups for many reasons, helping protect you against the following types of problems:

+   * Natural disasters such as fires, floods, and earthquakes that destroy computer systems
* Hardware failures in disk drives or other storage media that make it impossible to access the data they contain
* System software problems such as filesystem corruption that might cause files and directories to be deleted during filesystem consistency checks
* Software failures such as programs that crash or delete the files that you're working on
* Pilot error, the accidental deletion of important files and directories

# Note

Many people tend to confuse RAID (Redundant Array of Inexpensive Disks) with backups. They are not the same thing. RAID arrays can be a valuable asset in keeping your existing data online and available in the face of disk failures, but they do not protect against any of the problems identified in the previous list. All of the drives in a RAID array will burn even in case of a fire or other natural disaster.

In addition to protecting you against these sorts of problems affecting the data that they, and any other users of your systems require, there are a variety of procedural and business reasons to back up the data on your computer systems. Complete and accurate backups provide: