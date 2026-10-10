are well documented, and it would appear easy to extend the functionality of mc for your system if you understand shell scripting and regular expressions. It is an excellent choice for file management on servers not running X.

![](bbox=[0.1, 0.19, 0.82, 0.53])

**FIGURE 13.4** The Midnight Commander is a highly versatile file tool. If it does not display properly on your screen, launch it with the -a argument to force ASCII mode.

# ## System Rescue

There will come a time when you need to engage in system rescue efforts. This need arises when the system will not even start Linux so that you can recover any files. This problem is most frequently associated with the boot loader program or partition table, but it could be that critical system files have been inadvertently deleted or corrupted. If you have been making backups properly, these kinds of system failures are easily, although not quickly, recoverable through a full restore. Still, valuable current data might not have been backed up since the last scheduled backup, and the backup archives could not found to be corrupt, incomplete, or missing. A full restore also takes time you might not have. If the problem causing the system failure is simply a damaged boot loader, a damaged partition table, a missing library, or misconfiguration, a quick fix can get the system up and running and the data can then be retrieved easily.

This section first examines a way to back up and restore the boot loader itself or, having failed to do that, restore it by hand. It then looks at a few alternatives to booting the damaged system so that you can inspect it, fix it, or retrieve data from it.