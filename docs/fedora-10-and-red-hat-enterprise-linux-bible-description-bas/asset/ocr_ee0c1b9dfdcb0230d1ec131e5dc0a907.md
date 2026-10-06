486 Part III: Administering Fedora and RHEL

# # Deleting user accounts with User Manager

Delete a user from the User Manager window, simply click the line representing the user
account, and then click the Delete button.

+   * The information about the user is removed from the /etc/passwd file; thus, the user
no longer log in.
* The home directory and all files owned by the user will still exist. However, a listing of
files previously owned by that user (ls -l) will only show the former user's UID, but
no name, as the owner.

See the description in the previous section for information about how to find and remove
previously owned by the user.

# # Checking Disk Quotas

Limited disk space can be another source of user support. Fedora and RHEL offer the
software package for limiting and displaying the amount of disk space that a user can
consume. You can use the du command to see how much disk space has been used in a
particular directory (and related subdirectories). To automate the process of checking for disk
, you can create your own script. The following sections describe these ways of dealing
potential disk space problems.

# # Using quota to check disk usage

A careless or greedy user can gobble up all the space on your hard disk and, possibly, bring
your computer to a halt. By using quotas, you can limit the amount of disk resources a
user or group can use.

The quota package contains a set of tools that limit the amount of disk space (based
on disk blocks) and files (based on inodes) that a user can consume. Using quotas, you can
limit the amount of usage (on a per-user and -group basis) for each file system on your
computer. The general steps for setting disk quotas are:

+   1. Edit the /etc/fstab file.
2. Create quota files.
3. Create and start a quota startup script.
4. Create quota rules.
5. Check quotas.

You set quotas on file systems listed in your /etc/fstab file. For computers that are shared
 many users, there may be a separate /home or /var partition where users are expected
to put all their data. That kind of partition boundary can prevent an entire disk from being
consumed by one user. Quotas on the /home or /var partition can make sure that the space
within those partitions is shared fairly among your computer's users.