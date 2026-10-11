+   17. Log in as quotaboy or su over to his account:
+   
+   ```
+   su - quotaboy
+   ```

+   18. Run the quota command to see what quotaboy's usage is presently:
+   
+   ```
+   quota
+   Disk quotas for user quotaboy (uid 501):
+   Filesystem blocks quota limit grace files quota limit grace
+   /dev/sdb5    0   5000  6000      0     0   0   0
+   ```

+   19. As the quotaboy user, copy all the regular files in the /etc directory to the /data directory:
+   
+   ```
+   # cp /etc/* /data
+   ```

+   20. Run the quota command to see how many blocks are used and free:
+   
+   ```
+   Disk quotas for user quotaboy (uid 502):
+   Filesystem blocks quota limit grace files quota limit grace
+   /dev/sdb5    2524  5000  6000      152    0   0   0
+   ```

+   21. Fill up your quota by copying the entire /etc/ tree to the /data directory, observing the multiple errors about the disk quota being exceeded:
+   
+   ```
+   cp -r /etc /data
+   ```

+   22. Be sure to clean up the mess on your test system and try it again until you're comfortable with configuring quotas.

To ensure quotas are always on when users are on the system, add the **quotan** and **quotacheck** commands to a script and have the **/etc/rc.d/rc.sysinit** or similar script call them after the file systems are mounted.

# Hard and Soft Limits

Dissecting the edquota -u quotaboy editor session is important because there are several items that will be on the exam. Let's look at each section of the output:

```
Filesystem blocks soft hard inodes soft hard
/dev/sdb5    0     0   0     0   0   0
```

The sections are described here:

+   ▶ Filesystem—This is the file system on which the user has a quota.

+   ▶ blocks—This is the number of blocks presently used by the user on the file system in question.