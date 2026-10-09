# ## ACTIVITY 3-4

# ### Mounting Filesystems

**Before You Begin:**

+   1. You have logged in as root in the GUI.
2. Switch to the CLI.
3. At the command line, enter `useradd netadmin2` to create the user netadmin2.
4. Enter `passwd netadmin2` to set the password for netadmin2.
5. At the **New UNIX password** prompt, enter *mypy@$sw0rd* to set the password for netadmin2.
6. Confirm the password by retyping the same password at the prompt.
7. Enter `umount /dev/sdb5` to unmount the /dev/sdb5 partition.
8. Enter `umount /dev/sdb6` to unmount the /dev/sdb6 partition.
9. Enter `cd /root` to change to the root directory.
10. Enter `clear` to clear the terminal screen.

**Scenario:**

There is a meeting at your office. A couple of users want to have their systems moved to the conference room so that they can access their files during the conference. You find that there are multiple systems to be moved, and this will take a lot of time. Therefore, you decide to take the required files from the users and load them on the system in the conference room in separate partitions, so that the users can access their files.

Use the following user and partition details to mount the filesystems:

+   - User name: netadmin1, Partition size: 1 GB, Mount point: /admin1, User and group owner of /admin1: netadmin1
- User name: netadmin2, Partition size: 1 GB, Mount point: /admin2, User and group owner of /admin2: netadmin2

6