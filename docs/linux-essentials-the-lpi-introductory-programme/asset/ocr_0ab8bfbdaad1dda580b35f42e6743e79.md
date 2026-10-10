Net have no access to your important data (which might otherwise happen in spite of the user/administrator divide). With a little cunning you can even display a browser and e-mail program running under your “surfing account” among your “normal” programs\[1\].

Under Linux, every user account is assigned a unique number, the so-called user ID (or UID, for short). Every user account also features a textual user name (such as root or joe) which is easier to remember for humans. In most places where it counts—e.g., when logging in, or in a list of files and their owners—Linux will use the textual name whenever possible.

![](bbox=[0.1, 0.22, 0.14, 0.25])

The Linux kernel does not know anything about textual user names; process data and the ownership data in the file system use the UID exclusively. This may lead to difficulties if a user is deleted while he still owns files on the system, and the UID is reassigned to a different user. That user “inherits” the previous UID owner’s files.

![](bbox=[0.1, 0.3, 0.14, 0.34])

There is no technical problem with assigning the same (numerical) UID to different user names. These users have equal access to all files owned by that UID, but every user can have his own password. You should not actually use this (or if you do, use it only with great circumspection).

# **13.1.2 Users and Groups**

To work with a Linux computer you need to log in first. This allows the system to recognise you and to assign you the correct access rights (of which more later). Everything you do during your session (from logging in to logging out) happens under your user account. In addition, every user has a home directory, where only they can store and manage their own files, and where other users often have no read permission and very emphatically no write permission. (Only the system administrator—root—may read and write all files.)

![](bbox=[0.1, 0.51, 0.14, 0.55])

Depending on which Linux distribution you use (cue: Ubuntu) it may be possible that you do not have to log into the system explicitly. This is because the computer “knows” that it will usually be you and simply assumes that this is going to be the case. You are trading security for convenience; this particular deal probably makes sense only where you can stipulate with reasonable certainty that nobody except you will switch on your computer—and hence should be restricted by rights to the computer in your single-person household without a cleaner. We told you so.

Several users who want to share access to certain system resources or files can form a group. Linux identifies group members either fixedly by name or transiently by a login procedure similar to that for users. Groups have no “home directories” like users do, but as the administrator you can of course create arbitrary directories meant for certain groups and having appropriate access rights.

Groups, too, are identified internally using numerical identifiers (“group IDs” or GIDs).

![](bbox=[0.1, 0.75, 0.14, 0.78])

Group names relate to GIDs as user names to UIDs: The Linux kernel only knows about the former and stores only the former in process data or the file system.

Every user belongs to a primary group and possibly several secondary or additional groups. In a corporate setting it would, for example, be possible to introduce project-specific groups and to assign the people collaborating on those projects to the appropriate group in order to allow them to manage common data in a directory only accessible to group members.

¹Which of course is slightly more dangerous again, since programs running on the same screen can communicate with one another



![](bbox=[0.72, 0.15, 0.84, 0.18])

![](bbox=[0.72, 0.45, 0.84, 0.47])

![](bbox=[0.72, 0.65, 0.84, 0.66])