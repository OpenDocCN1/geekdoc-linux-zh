# 5
READ THIS BEFORE YOU BREAK SOMETHING
ELSE! (BACKUP AND RECOVERY)

![](bbox=[0.4, 0.26, 0.6, 0.4])

The most common cause of system failure is those pesky humans, but hardware and operating systems also fail. Hackers learn new ways to disrupt networks and penetrate applications, and you'll inevitably need to upgrade and patch your system on a regular basis. (Whether or not you *will* upgrade and patch is an entirely separate question.) Any time you touch a system, there's a chance you'll make a mistake, misconfigure a vital service, or otherwise totally ruin your system. Just think of how many times you've patched a computer running any OS and found something behaving oddly afterward! Even small system changes can damage data. You should, therefore, always assume that the worst is about to happen. In our case, this means that if either the hardware or a human being destroys the data on your hard drive, you must be able to restore that data.

We'll start with system backups and managing tape drives using tar(1) and then review recording system behavior with script(1). Finally, should you suffer a partial or near-total disaster, we'll consider recovering and rebuilding with single-user mode and the install media.

# **System Backups**