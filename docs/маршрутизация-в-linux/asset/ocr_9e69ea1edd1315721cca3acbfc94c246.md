```
pruning on
phyint 199.60.103.90 disable
phyint 199.60.103.91 rate_limit 60 threshold 10 \
preference 1029 boundary multi
phyint 199.60.103.92 rate_limit 60 threshold 10 \
preference 1024 boundary multi
tunnel 199.60.103.92 216.17.105.9 rate_limit 60 \
threshold 10 preference 1024 boundary multi
```

# Running mrouted

After you’ve set up the configuration file, you’re ready to run the DVMRP daemon, mrouted. The usual recommendations apply, such as setting up the daemon to start and stop automatically at boot and shutdown, but not until you’ve run it manually at first to determine what combination of flags and settings works best for your needs. The format for running this daemon is

```
mrouted flags
```

Yes, that’s it. The available flags are

+   - -p. Disable tree pruning.
+   - -c file. Utilize the specified configuration file. Be sure to include the path in file.
+   - -d. Enter debug level 2. The debugging levels are outlined in Table 6.1.
+   - -d level. Enter the specified debug level.

# Table 6.1 Debugging Levels Available in mrouted

| Level | Description |
| --- | --- |
| 1 | Send all syslogd messages to STDERR. |
| 2 | Level 1 plus send all messages marked "significant" to STDERR. |
| 3 | Level 2 plus send messages recording every packet’s arrival and departure to STDERR. |

# Summary

You have a number of options available to you in the multicasting daemon world. If you want to set up wide-scale or internal multicasting, then typically you’ll want to use PIM-SM to carry your traffic—or even PIM-DM if you have a very dense local setup. One simple method of setting up PIM-SM is to utilize pim6d, a nice little single-function daemon. On the other hand, if you need to connect to the mbone, you have to use DVMRP, for which you have mrouted. You also can choose options such as getting access to the multicast gated, the multicast components of zebra when they are available, or try one of the additional options that will no doubt appear as multicasting gains ground. Considering the amount of bandwidth that unicasting data such as Internet radio consumes, those days aren’t too far off.