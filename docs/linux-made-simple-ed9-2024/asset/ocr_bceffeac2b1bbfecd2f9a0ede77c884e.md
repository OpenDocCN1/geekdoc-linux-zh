file properties in the Terminal using the **ls -l** command to list the content of a folder.

![](bbox=[0.44, 0.08, 0.86, 0.16])

# Folder versus file

Things are complicated further because setting permissions on files is only half the story. The file’s parent folder plays a crucial role too, because if you deny access to the folder by not granting the execute (x) permission, then it doesn’t matter what file permissions you set, the files themselves are kept out of reach, so you can’t view, edit or execute them.

On the flip side of the coin, if you have a file that you’ve denied write access to, you might think that would protect it from being erased. In fact, the permission for deleting a file doesn’t rest with the file itself, but rather the directory it’s stored in. Set the folder to write (w) access, and the file can be deleted, regardless of what permissions you set on it.

# Owners, users and everyone else

Ubuntu is all about security, so rather than apply a single set of permissions to each file and folder on your system, Linux applies permissions to three separate categories, giving you more granular control over who has what level of control. The first is the owner of the file, which by default is the user who created the file in question.

The second category refers to a single user group for whom specific permissions have been defined, and opens up a question about users and groups. Although it appears to apply to a specific user (often the same user as the file or folder’s owner), this set of permissions actually applies to a user group.

When you create a new user, a group of the same name is also created, your user is added to that group and it’s actually this group that Linux references here. It’s also possible to add users to multiple groups, allowing advanced users to set up groups into which multiple users are added, giving all those users the same level of access to the selected file or folder based on the group they’re part of.

The third and final category is a catch-all ‘everyone else’ group, which applies to all other users on your PC who aren’t covered by the first two categories.

How are permissions set? When a file is created, it’s automatically owned by the user that created it, whether that’s your own user profile or – if you’ve created it through the sudo command – the root user. The owner is also automatically set as the default user or group. The owner typically has full access rights to the file or folder created, while ‘everyone else’ normally has more limited rights to files, and are usually blocked from folders.

This approach forms the cornerstone of security on your Linux file system. By default, all users have full ownership, access and control over their personal Home folder and its contents, while other users are blocked access. Outside the home folder, access is more restrictive – certain folders are accessible, but most are either read-only or off-limits completely, requiring you to access them via the ‘root’ superuser account.

folder or file in question, right-click it and choose Properties. Switch to the Security tab and use the annotation above to help guide you through what’s what.

It’s worth noting a few things here. First, you can only change permissions for items you own, while the options on offer aren’t as flexible as those available when you edit permissions using the Terminal. On the other hand, it’s a much easier way to quickly check the permissions of an object and take remedial action if you think there’s something awry.

Another thing; you can also change the file’s group here. Click the dropdown menu and you’ll see a list of users you won’t recognise in addition to any users you’ve set up yourself – these are specially created system users, designed to do specific things without compromising on security. There’s no reason to use these groups in the context of file and folder permissions, so leave them well alone.

In fact, it’s probably a good idea to avoid messing about with permissions unless you know exactly what you’re doing. Nautilus makes it impossible for you to lock yourself out of your own files by changing the file owner, but you can still quickly and easily get lost among the various options on offer.

That said, if you do want to learn about wielding complete control over permissions, users and groups – including the ability to assign users to different groups – you’ll need to get your hands dirty in the Terminal. For more help and advice in this area, check out our tutorial on page 136.

Check the permissions for any file or folder using the ls -l command in a Terminal window.

> **Quick tip**
> 
> If you connect to a drive that isn’t formatted using the file system, then permissions for all of its files and folders are determined when you mount it. Read/write by default, but read-only is also an option.

# View and change permissions

We’ve seen how you can use the **ls -l** command in the Terminal to view the permissions of a file or folder. Doing so not only reveals the permissions for each category, but also the name of the file owner and the group that has special access rights.

If you’d prefer a more user-friendly view, plus want limited access to changing permissions for any reason, browse to the

![](bbox=[0.44, 0.6, 0.77, 0.83])

The Public folder is a good place to share files with other users of your PC on a read-only basis.