If you click Add to create a new group, you are presented with the screen in Figure 9-28. Here you can enter the group name, the group ID (it is safe to use the default), and also the option to use a password for the group.

![](bbox=[0.176, 0.206, 0.673, 0.506])

Figure 9-28: Adding a new group to the system

Users are able to change their default group for a session by using the newgrp command. For example, if just wants to change his default group from users (the default) to dev, he can use the command newgrp dev. If a password is set for this group, he must enter it before he can change to this new group.

If you want to add any users to this group, you can select them from the right-hand pane. When you are happy with the new group, click Next. Now you are returned to the group list, where you will see your new group in the list. Click Finish to return to YaST.

# # Installing Additional Software with YaST

Unless you install every available package when you installed your SUSE system, you'll eventually hear (or read about) some additional software package from the SUSE distribution CDs or DVD that you wished. Chapter 12 explains how to install additional software packages from the command line, but if this is on the SUSE distribution CDs or DVD, you'll have to figure out where to find it first. Luckily, SUSE's YaST tool makes it easy to both locate and install additional software from your SUSE distribution media.