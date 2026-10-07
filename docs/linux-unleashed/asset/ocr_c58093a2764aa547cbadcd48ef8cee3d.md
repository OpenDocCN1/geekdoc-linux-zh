If you do rely on auditing, you should scan the logs often. It might be worthwhile to write a quick summary script program that totals the amount of time each user is on the system so that you can watch for anomalies and numbers that don’t mesh with your personal knowledge of the user’s connect times. A simple shell script to analyze the log can be written in gawk. In addition, some audit reporting systems are available in the public domain.

# Preparing for the Worst

Assuming someone does break in, what can you do? Obviously, backups of the system are helpful because they let you recover any damaged or deleted files. But beyond that, what should you do?

First, find out how the invader got in, and secure that method of access so it can’t be used again. If you’re not sure of the access method, close down all modems and terminals and carefully check all the configuration and setup files for holes. There has to be one, or the invader couldn’t have gotten in. Also check passwords and user lists for weak or outdated material.

If you are the victim of repeated attacks, consider enabling an audit system to keep track of how intruders get in and what they do. As soon as you see an intruder log in, force him off.

Finally, if the break-ins continue, call the local authorities. Breaking into computer systems (whether in a large corporation or a home) is illegal in most countries, and the authorities usually know how to trace the users back to their calling point. They’re breaking into your system and shouldn’t get away with it!

# Summary

Following the simple steps outlined in this chapter will give you enough security to protect your systems against all but the most determined and knowledgeable crackers. You can’t do any harm with the steps mentioned, so you may as well perform them for all Linux systems that have modems or network connections. From here, you can learn about the following topics:

+   Setting up the Network File System is discussed in Chapter 43, “NFS.”
Backups are discussed in Chapter 45, “Backups.”
What’s involved in setting up your Linux system as a Web server is discussed in Chapter 47, “Setting up an Internet Site.”
Modifying the kernel is discussed in Chapter 57, “Working with the Kernel.”