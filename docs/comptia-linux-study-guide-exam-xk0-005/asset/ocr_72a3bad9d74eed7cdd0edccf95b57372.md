You can, however, modify the soft and hard limits for both blocks and inodes. When you set a hard block limit, you are setting the maximum number of blocks the user can fill with data. When you set inode hard limits, you are setting the total number of files that the user can create. Once the user hits either of these limits, no more disk space or file creation is available for that account on this particular filesystem. Note that if set to 0, the limit is disabled. Notice in Listing 10.36 that inode limits are disabled.

Soft limits are a little nicer. Once the user hits a set soft limit, they can go for an extended period past this limit. It is called a grace period.

Once you have user (or group) quotas modified, you need to establish the grace period for any soft limits set. To do this, you use the edquota -t command. These grace periods are used for all users and groups. An example is shown in Listing 10.37.

# **Listing 10.37:** Employing edquota -t to set soft limit grace periods

```
# edquota -t
Grace period before enforcing soft limits for users:
Time units may be: days, hours, minutes, or seconds

  Filesystem  Block grace period  Inode grace period
  /dev/sdb1        7days           7days
~
```

When you issue the edquota -t command, you are again thrown into the vim editor, unless you have modified the $EDITOR environment variable. Grace periods can be set for both blocks and inodes and can be a matter of days, hours, minutes, or even seconds, which doesn't seem very graceful.

> If you have some sort of odd problem when enabling filesystem quotas, you can quickly turn them off with the quotaoff command, using super user privileges. The -a option will allow you to turn them off for all the system's quota-enabled filesystems. You will need to specify user quotas (-u) and/or group quotas (-g) in the command. Once you have fixed the issues, turn filesystem quotas back on using the quotaon command.

When you have modified a user's quota limits and set grace periods, it's a good idea to double-check your modifications. The quota command can help here. An example is shown in Listing 10.38.

# **Listing 10.38:** Using quota to check a user's quota limits

```
# quota -u user1
Disk quotas for user user1 (uid 1000):
  Filesystem  blocks  quota  limit  grace  files  quota  limit  grace
  /dev/sdb1     212  4096  6144        2     0      0
#
```