# # ACTIVITY 3-5
Maintaining the Linux Filesystem

**Before You Begin:**

+   1. You have logged in as root in the CLI.
2. Enter `telinit 3` to switch to runlevel 3.
3. Press `Enter` to continue in the new runlevel.
4. Enter `clear` to clear the terminal screen.

**Scenario:**

Due to a thunderstorm, there was a brief power outage overnight and the Linux systems were not shutdown properly. The systems need to be checked for consistency. Using the `fsck` command, verify the drive and data integrity of the hard disk.

| **What You Do** | **How You Do It** |
| :--- | :--- |
| 1. Run the `fsck` command on the local filesystem. | a. Enter `telinit 1` to switch to single-user mode.<br>b. Enter `fsck /dev/sdb1`<br>c. At the warning prompt, press Y and then press `Enter`.<br>d. Observe that the message displays "clean", which indicates that there is no error in the filesystem.<br>e. Enter `telinit 3` to switch to runlevel 3. |
| 2. At which runlevel can you perform disk maintenance without damaging the disks? | a) Runlevel 0<br>\checkmark b) Runlevel 1<br>c) Runlevel 3<br>d) Runlevel 5 |
| 3. True or False? You can run the e2fsck command to perform a disk check on a mounted filesystem. | \underline{~~} True<br>\checkmark\underline{} False |