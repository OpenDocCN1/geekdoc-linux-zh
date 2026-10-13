2. The first change we need to make is to edit /etc/vfstab (notice that it's not fstab, but vfstab) to add rq to the list of mount-time options. Then, instead of creating quota.user and quota.group, simply create a single file quotas:

```
# cd /export/home
# touch quotas ; chmod 600 quotas
```

Now, unmount the disk and remount it; then use edquota to set up a quota for a user. The edquota command is essentially the same, even though the actual layout of the information presented in the editor is slightly different.

3. next, ensure all is set up properly with quotacheck. The Solaris version of quotacheck differs in what flags it understands. To get the equivalent of the -aguv set in Linux, use -pva, which has the added benefit of checking quotas in parallel, which can be considerably faster!

```
# quotacheck -pva
*** Checking quotas for /dev/rdsk/c0d0s7 (/export/home)
#
```

The repquota reports the status of users on a device with quotas enabled:

```
# repquota -a
/dev/dsk/c0d0s7 (/export/home):

               Block limits          File limits
User   used  soft   hard  timeleft   used  soft  hard  timeleft
taylor  0   5000   7500            0     0     0
```

4. Here's what user taylor would see on a Solaris box by using quota:

```
$ /usr/sbin/quota
$
```

Remember, without the -v flag it only reports systems where the user is over quota.
One more try:

```
$ /usr/sbin/quota -v
Disk quotas for taylor (uid 100):
Filesystem  usage  quota  limit  timeleft  files  quota  limit  timeleft
/export/home  0   5000   7500          0     0     0
```

Many system administration books counsel you not to bother with disk quotas because they're obsolete or no one really uses them. I disagree. If you have a multiuser system, it's in everyone's best interest to set high, but meaningful, disk quotas to ensure that the resources are shared fairly. If you set this up prior to assigning accounts, you'll never have to argue with sore users afterward either!