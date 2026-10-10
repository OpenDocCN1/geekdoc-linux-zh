Either form will work. If `flagshg:/home/timothy/files` is mounted automatically (from a listing in `/etc/fstab`), the directory will be remounted the next time you boot CentOS. If it was a temporary mount (or listed as `noauto` in `/etc/fstab`), it will not be remounted at boot time.

> **TIP** The command is not `unmount`, it is `umount`. This is easy to get wrong.

If you get the message "device is busy" when you try to `umount` a file system, it means that the `umount` fails because the file system is being accessed. Most likely, one of the directories in the NFS file system is the current directory for your shell (or the shell of someone else on your system). The other possibility is that a command is holding a file open in the NFS file system (such as a text editor). Check your Terminal windows and other shells, and `cd` out of the directory if you are in it, or just close the Terminal windows.

If an NFS file system won't `umount`, you can force `umount` it (`umount -f /media/flashg`) or `umount` and clean up later (`umount -l /media/flashg`). The `-1` option is usually the better choice because a forced `umount` can disrupt a file modification that is in progress.

# Other Cool Things to Do with NFS

You can share some directories to make it consistent for a user to work from any of several different Linux computers on your network. Some examples of useful directories to share are:

+   **`/var/spool/mail`** — By sharing this directory from your mail server and mounting it on the same directory on other computers on your network, users can access their mail from any of those other computers. This saves users from having to download messages to their current computers or from having to log in to the server just to get mail. There is only one mailbox for each user, no matter where it is accessed.

+   **`/home`** — This is a similar concept to sharing mail, except that all users have access to their home directories from any of the NFS clients. You would mount `/home` on the same mount point on each client computer. When the user logs in, that user has access to all the user's start-up files and data files contained in `/home/user/directory`.

> **TIP** If your users rely on a shared `/home` directory, you should make sure that the NFS server that exports the directory is fairly reliable. If home isn't available, the user may not have the start-up files to log in correctly or any of the data files needed to get work done. One work-around is to have a minimal set of start-up files (`.bashrc`, `.Xdefaults`, etc.) available in the user's home directory when the NFS directory is not mounted. Doing so allows the user to log in properly at those times.

+   **`/project`** — Although you don't have to use this name, a common practice among users on a project is to share a directory structure containing files that people on the project need to share. This way everyone can work on original files and keep copies of the latest versions in one place. (Of course, a better way to manage a project is with CVS or some other version control-type software, but this is a simple work-around.)