4. Check the time again. Type hwclock and press Enter. The time kept by the hardware clock is now set to the time stored in the BIOS clock:
Sat Jul 1 10:00:37 2000 -0.693272 seconds
The time that displays in this example is almost the correct time, at 10 a.m. on Saturday, July 1, 2000. The clock is just a few minutes off.

5. If the time is still wrong, set the time manually. Use the following command syntax
hwclock --set --date="MM/DD/YY HH:MM:SS"
For example, to set the time to 10:15 a.m. on July 1, 2000, type hwclock --set --date="07/01/00 10:15:00" and press Enter.

6. Check the time again. Type hwclock and press Enter.

# Summary

You now have a few tools under your belt to help you manage your hard drive space. In the past hour, you learned how to determine which files and users were using more than their fair share of disk space. You also learned a few tricks for keeping free space at a desirable level.

# Q&A

Q How do I scan my hard drive for errors?
A Every time you boot the Linux operating system, the startup process automatically checks the hard drive for errors with the fsck command. If you want to use the fsck command, you need to unmount the filesystem that you want to check before running this command. To learn more about the fsck command, read the manual page (type man fsck at the shell prompt).

Q If I limit the amount of disk space that is available to an individual user, is there any way I can notify him or her?
A You can always tell users that you are limiting the amount of space available to them to store files and let them know what limits you set. The users can then use the du command to see how close they are coming to their limit. Another way is to use the edquota -t command. This allows you to automatically notify users that they have used up their disk space quota. The edquota -t command opens a file in the vi text editor, and you will need to specify the number of days the users can go over their limit. After the grace period, users will not be able to add any new files to their home directories.