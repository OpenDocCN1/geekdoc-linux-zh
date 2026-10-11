# # Special File Permissions

Several facts about how the Linux and Unix file systems are constructed can cause problems for administrators. The first interesting factoid is that because only a single group can be the group owner for a given object, who-ever wants access to that object has to be a member of the owning group.

![](bbox=[0.08, 0.23, 0.18, 0.31])

> Yes, there are now access control lists (ACLs) on some Linux systems and in a few distributions, but not on the exam, so be very careful when considering special bit and group ownership questions.

Trying to configure many groups and users to have access to the right files can be difficult. Every user has a primary group and secondary groups, and you must make sure that every user who shares data in a given directory has the same primary group. That’s nearly impossible beyond 10 or so users. There’s a way out of this situation: You can set an additional or special bit on the shared directory, which causes all users who have access to inherit the group owner of the directory on all their created objects.

Secondly, although Linux has a limited set of permissions, in some situations special bits must be used to allow users who aren’t any kind of owner of an object to access that object. (If this sounds like a security risk, it is, but stay tuned and I’ll explain this.)

# ## Special Bit Permissions

The following special bits are available for Linux file system use:

+   > **SUID**—The Set User ID allows users to run a program as if they were the owner, be it another user or root (numeric = 4000).

+   > **SGID**—The Set Group ID allows you to apply group permissions to a set of files, making shared directories and data possible (numeric = 2000).

+   > **Sticky bit**—Save Text mode used to be for keeping programs in mem-ory to speed access, but now it’s used to keep nonowners from deleting files in a common directory (numeric = 1000).

Remember that these bits are used when necessary, which isn’t often, and they are a security risk, even when properly used. Additionally, any user who can copy a file can change that file, but the SUID and SGID bits are stripped off any copied file for security.

Special bits can be set either of two ways—numeric or symbolic, much like setting other permissions with chmod.