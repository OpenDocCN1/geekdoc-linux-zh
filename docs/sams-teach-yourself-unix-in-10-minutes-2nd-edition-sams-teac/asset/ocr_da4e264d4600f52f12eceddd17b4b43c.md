# Configuring Permissions in Unix 213

# Using chmod

Now that you know permissions are, you probably want to know how to change them, because listing them can only get you so far. Listing them will help you to get a good grip on what is there, but to make changes you need to take the next step, which is to use the chmod command. There are two modes of operation that you can use with chmod: a quick-and-dirty mode, and a more user-friendly mode of setting permissions.

The user-friendly mode uses easy-to-remember commands to set or unset permissions. To use this, do the following:

+   1. **Pick a permission level.** If you want to set permissions for the owner, the level is u. If you want to change permissions for the group, it is g. For other permissions, choose o. Lastly, if you want to affect all the levels of permissions (owner, group, and other), use a.
2. **Choose an operation.** Decide whether you want to set (turn on) or unset (turn off) a particular level of permission. If you want to set a permission, the operation is +; if you want to unset a permission, it is -.
3. **Choose the permission itself.** If you want to operate on the read permission, choose r, for write choose w, and for execute x.
4. Issue the chmod command in this manner: chmod <permission level><operation><permission> <filename> <filename>

Let's look at an example of chmod in action. It is important that you pay close attention to this lesson and to walk away with this knowledge you are moving from end user to system administrator. Not knowing how to set permissions will almost always ruin your chances for advancement because you will not be able to do anything without knowing how to change permissions.