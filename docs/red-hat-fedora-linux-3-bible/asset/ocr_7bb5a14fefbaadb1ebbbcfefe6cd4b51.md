+   3. Next, you could try going straight to the shared directory. For example:
+   
+   ```
+   $ cd /net/shuttle/usr/local/share
+   $ ls
+   info man music television
+   ```

At this point, the ls should reveal the contents of the /usr/local/share directory on the computer named shuttle. What you can do with that content depends on how that content was configured for sharing by the server.

# Unmounting NFS file systems

After an NFS file system is mounted, unmounting it is simple. You use the unmount command with either the local mount point or the remote file system name. For example, here are two ways you could unmount maple:/tmp from the local directory /mnt/maple.

```
# umount maple:/tmp
# mount /mnt/maple
```

Either form will work. If maple:/tmp is mounted automatically (from a listing in /etc/fstab), the directory will be remounted the next time you boot Fedora. If it was a temporary mount (or listed as noauto in /etc/fstab), it will not be remounted at boot time.

> TIP: The command is not unmout, it is umount. This is easy to get wrong.

If you get the message device is busy when you try to umount a file system, it means the umount fails because the file system is being accessed. Most likely, one of the directories in the NFS file system is the current directory for your shell (or the shell of someone else on your system). The other possibility is that a command is holding a file open in the NFS file system (such as a text editor). Check your Terminal windows and other shells, and cd out of the directory if you are in it, or just close the Terminal windows.

If an NFS file system won't unmount, you can force umount (i umount -f /mnt/maple) or unmount and clean up later (umount -l /mnt/maple). The -l option is usually the better choice, because a force umount can disrupt a file modification that is in progress.

# Other cool things to do with NFS

You can share some directories to make it consistent for a user to work from any of several different Linux computers on your network. Some examples of useful directories to share are:

+   - /var/spool/mail — By sharing this directory from your mail server, and mounting it on the same directory on other computers on your network, users can access their mail from any of those other computers. This saves users from having to download messages to their current computers or from having to log in to the server just to get mail. There is only one mailbox for each user, no matter from where it is accessed.