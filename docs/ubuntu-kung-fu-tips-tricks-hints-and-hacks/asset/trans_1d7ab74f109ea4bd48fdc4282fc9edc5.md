

![](img/48d064407ff591f0b5365c2d2919ee6e_99_0.png)

Figure 5-1. File/folder permissions.

with a file. There are a handful of other letters that can appear here, but the main one you’ll encounter is l, which indicates a link.

Following this are the three sets of permissions, listed one after the other: rwxr-xr-x. After that is a link number, which isn’t relevant to this discussion and can be ignored. Then the owner’s username is listed (in this case, keir), and then the group the file is assigned to (the group is also called keir).

> NOTE Under Ubuntu each user is assigned to their own personal group, that is named after their username. This policy effectively means that group permissions are irrelevant for personal files unless you were specifically to add another user to your personal group. However, it’s still important you understand the concept of groups and how it applies to file/folder permissions.

Here are the permissions separated out into sets of three relating to owner, group and others:

- Owner: rwx
- Group: r-x
- Others: r-x

The owner has read (r), write (w), and execute (x) permissions. In other words, he can do anything—he has full permissions. He can view a file listing of the Desktop folder, and write new files there. He can switch to the folder by typing cd Desktop, or by browsing to it with Nautilus.

Members of the group keir have read and execute permissions, so they can view a file listing of the folder, and also switch into it. However, they can’t write any files there, or delete them, because there’s a hyphen where the w would normally appear. Quite simply, a hyphen in place of a permission means “no permission”.

Finally, other users on the system also have read and execute permissions, but not write permissions—just like with the group permissions.

Let’s take a look at another example of permissions, this time from a word processing document called `report.doc`:

```
-rw-r--r-- 1 keir keir 3024 2008-10-28 18:21 report.doc
```

Once again, we see that the file belongs to the user named `keir`, and is assigned to the group named `keir`.

This time the permission component of the listing starts with a hyphen, because this is a file and not a folder or link. Following this are the three groups of permissions that again can be split-out as follows:

```
Owner: rw-
Group: r--
Others: r--
```

The first permission grouping refers to the owner, and he can read and write to the file, but not execute it. That makes sense because this is a document file and not a program; nobody would want to execute it.

Next, the group permissions say that any member of the group called `keir` can read the file, but not write changes to it (there’s a hyphen where the w would be), or execute it.

Finally, others on the system can also read the file, but not write changes to it or execute it.

In other words, for everybody but the user named `keir`, the file is read-only.

## Changing ownerships and permissions

Files or folders can have their ownership and group reassigned, but root powers are usually needed to do so.

> **NOTE** A user can reassign the file’s group without root powers, but only if they’re a member of that group.

The owner of a file or folder can change its permissions so that read, write and execute permissions are either added or removed. Root powers aren’t needed for this.

### Changing file ownership and group assignment

The `chown` (change owner) command is used to change a file or folder’s ownership. It must be preceded by `sudo`, because changing a file or folder’s ownership requires root powers.

The following will switch ownership of the file `report.doc` to the user `frank`:

- `sudo chown frank report.doc`

The `chgrp` (change group) command is used to reassign a file or folder’s group. The following assigns the file `report.doc` to the `accounts` group:

- `sudo chgrp accounts report.doc`

However, you can reassign the owner and group in one fell swoop by using `chown` and separating the new owner and group assignment with a colon. The following will change the ownership of `report.doc` to `frank`, and change the group assignment to `accounts`:

- `sudo chown frank:accounts report.doc`

### Changing file permissions

The `chmod` (change mode) command is used to alter permissions.

There are various ways of using the `chmod` command, but the easiest is to first specify who you want to alter the permission for (owner, group, or others) and then specify the permission changes (i.e. whether to add/remove read, write or execute permissions). Following this, the file or folder name should be specified.

Whom permissions should be changed for is indicated by `u`, `g` or `o`, standing for user (i.e. owner), group or others. The letter `a` can be used to indicate all three.

The permissions are indicated by `r`, `w` or `x` for read, write or execute, and whether the permission should be added or removed is indicated by the use of a plus or minus symbol (`+/-`).

Let’s go back to the file `report.doc` that, you may recall, had the following permissions and user/group ownerships:

```
`rw-r--r-- keir keir`
```

The owner can read/write to the file, but everybody else (group and others) can only read the file.

If we wanted to allow members of the group to be able to write to the file, we could type the following:

- `chmod g+w report.doc`

In other words, this adds (+) write permissions (w) for `report.doc`’s group (g).

If we were feeling generous and wanted to let other users to write to it too, we could type the following:

- `chmod o+w report.doc`

