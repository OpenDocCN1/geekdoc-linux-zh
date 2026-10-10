# Tip

You may want to back up a user's home directory before deleting it. This way, you can restore a user's account if you discover it shouldn't have been deleted, or if the individual comes to you with a request for recovery of files from the account.

If you don't provide a username on the command line with **rmuser**, the utility prompts you for one when you type the command.

# Deleting Users from /etc/master.passwd

On rare occasion, you might want to delete a user from the computer but not perform all of the tasks that **rmuser** normally performs. For instance, you might want to keep the user's group for use by users you plan to add shortly, or keep a user's *temporary* files for use by others. In such situations, you can delete a user account by manually performing each of the steps described in "Using **rmuser**" that you do want to perform. The most important of these is removing the account from the password database files. You can do this by editing `/etc/master.passwd` and then using the **pwd_mkdb** utility, described in the previous section, "Editing `/etc/master.passwd`." Delete the line in this file relating to the user and then run **pwd_mkdb**:

```
`# pwd_mkdb -p /etc/master.passwd`
```

This procedure will recreate your password database without the user, effectively removing the account. Several files associated with the now-unused UID will still remain, though, and these could cause confusion in the future. If you reuse the UID, new users might find the old user's mail, for instance, possibly including confidential information.

# Removing Stray User Files

Although **rmuser** makes an effort to remove all the files belonging to a user, it's not always successful. Problems are particularly likely to crop up if your system includes shared file directories in which collaborating users can store files. You can search for such files using the **find** utility, which was described in Chapter 8. Specifically, you can use the -user *uname* option, where *uname* is a username (if you run the command before deleting the user) or a UID. For instance, consider the following command:

```
`# find /home -user 1003`
```

This command finds all files in the /home directory tree that belong to UID 1003. You can then delete these files or use chown (also described in Chapter 8) to reassign ownership of these files to other users. Failing to perform this step won't make the files unusable to others, although others might be unable to modify these files or delete files in directories owned by the now-deleted user, depending upon permissions.