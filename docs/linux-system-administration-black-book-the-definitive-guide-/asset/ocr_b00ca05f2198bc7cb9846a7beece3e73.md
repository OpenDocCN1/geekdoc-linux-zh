# Incremental Backup With Redundancy

If you have the time and inclination, it is wise to build some form of redundancy into your backup scheme. As discussed in the section “Introduction To Backup Schemes,” there are many reasons to have redundant backups—everything from not catching an error that perpetuates for several days or weeks to an intruder who makes fundamental changes that have to be reversed.

When you begin adding redundancy to a backup scheme, the first thing you might notice is that many more backup media are required. This fact occurs because you will be keeping more copies of previous backups instead of overwriting the backups each time.

Another difference is in the form of reminders. A redundant backup scheme, by its very nature, is more complex to keep track of. It is important to put together a reminder setup, so that you remember which tapes to put in on which days.

One method you might use for implementing an incremental, redundant backup scheme is called the Tower of Hanoi:

+   • Day 1—Use a new reusable media to make a backup. Mark it “1”.
+   • Day 2—Use a new reusable media to make a backup. Mark it “2”.
+   • Day 3—Use the “1” media to make your backup.
+   • Day 4—Use a new reusable media to make a backup. Mark it “3”.
+   • Day 5—Use the “1” media to make your backup.
+   • Day 6—Use the “2” media to make your backup.
+   • Day 7—Use the “1” media to make your backup.
+   • Day 8—Use a new reusable media to make a backup. Mark it “4”.
+   • Day 9—Use the “1” media to make your backup.
+   • Day 10—Use the “2” media to make your backup.
+   • Day 11—Use the “1” media to make your backup.
+   • Day 12—Use the “3” media to make your backup.
+   • Day 13—Use the “1” media to make your backup.
+   • Day 14—Use the “2” media to make your backup.
+   • Day 15—Use the “1” media to make your backup.
+   • Day 16—Use a new reusable media to make a backup. Mark it “5”.
+   • Day 17—Return to Day 1.

![](bbox=[0.91, 0.25, 0.99, 0.42])