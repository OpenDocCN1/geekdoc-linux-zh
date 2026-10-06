# Unmounting NFS File Systems

After an NFS file system is mounted, unmounting it is simple. You use the unmount command with the local mount point or the remote file system name. For example, here are two ways you can unmount maple:/tmp from the local directory /mnt/maple.

```
# umount /tmp
# umount /mnt/maple
```

Other forms work. If maple:/tmp is mounted automatically (from a listing in /etc/fstab), the directory will be remounted the next time you boot Linux. If it is a temporary mount (or listed as noauto in /etc/fstab), it won't be remounted after boot.

> The command is unmount, not unmount. This is easy to get wrong.

If you get the message device busy when you try to unmount a file system, the unmount failed because the file system is being accessed. Most likely, one of the directories in the NFS file system is the current directory for your shell (or the shell of some else on your). The other possibility is that a command is holding a open file in the NFS file system (such as a text editor). Check your Terminal windows and other shells, and cd out of the directory if you are in, or just close the Terminal windows.

If an NFS file system won't unmount, you can force it (umount -f /mnt/maple) or unmount and clean up (umount -l /mnt/maple). The -l option is usually the best choice because a forced unmount can disrupt a file system that is in progress.

# Other Cool Things to Do with NFS

You can share some directories to make it convenient for a user to work from any of different computers on your network. Some examples of useful directories to share:

+   /var/spool/mail — By sharing this directory from your mail server and mounting it on the same directory on other computers on your network, users can access their mail from any of other computers. This saves users from having to download messages to their current computers or having to log in to the server to get mail. There is only one mailbox for each user, no matter where it is accessed.

+   /home — This is a similar concept to sharing mail, except that all users have access to their home directories from any of the NFS clients. Again, you would