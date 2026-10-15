to create them, and any other information you would need to restore the system without referring to on-line documentation.

Free and commercial labeling programs abound. Save yourself a major headache and invest in one. Vendors of laser printer labels can usually provide templates for each of their labels. Better yet, buy a dedicated label printer. They are inexpensive and work well.

Your automated dump system should record the name of each filesystem it has dumped. Good record keeping allows you to quickly skip forward to the correct filesystem when you want to restore a file. It’s also a good idea to record the order of the filesystems on the tape or case.

If you can afford it, buy an autchanger or tape drive that reads bar codes. This feature ensures that your electronic tape labels always match the physical ones.

# Pick a reasonable backup interval

The more often backups are done, the less data is lost in a crash. However, backups use system resources and an operator’s time. You must provide adequate data integrity at a reasonable cost of time and materials. In general, costs increase as you move toward more granular restoration capabilities.

On busy systems, it is generally appropriate to back up home directories every workday. On systems that are used less heavily or on which the data is less volatile, you might decide that performing backups several times a week is sufficient. On a small system with only one user, performing backups once a week is probably adequate. How much data are your users willing to lose?

# Choose filesystems carefully

Filesystems that are rarely modified do not need to be backed up as frequently as users’ home directories. If only a few files change on an otherwise static filesystem (such as /etc/passwd in the root filesystem), you can copy these files every day to another partition that is backed up regularly.

If /tmp is a separate filesystem, it should not be backed up. The /tmp directory should not contain anything essential, so there is no reason to preserve it. If this seems obvious, you are in better shape than many sites we’ve visited.

# Make daily dumps fit on one piece of media

In a perfect world, you could do daily dumps of all your important filesystems onto a single tape. High-density media such as DLT, AIT, and LTO make this goal practical for some sites. However, as our work habits change and telecommuting becomes more popular, the range of “good” times to do backups is shrinking. More and more network services must be available around the clock, and large backups take time.

See Chapter 9 for more information about cron.