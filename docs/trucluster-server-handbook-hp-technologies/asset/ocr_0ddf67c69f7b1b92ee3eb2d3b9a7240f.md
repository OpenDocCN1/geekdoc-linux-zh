# 7.5.1.4 How Do I Fix a “second device status is active” Error?

Occasionally when you replace a device, the dfsl.dat and dfsc.dat files need to be updated; otherwise, when you attempt to rename the new device back to the old device special file, you will see the following:

```
# dsfmgx -m dsk7 dsk9
dsfmgr: ERROR: second device status is active: dsk9a
```

First, you will need to identify which HWID is associated with dsk9. You will probably already know which it is, because you probably deleted the component when you replaced the device. If you do not know the HWID, however, you can still find it by searching the dfsc.dat file.

```
# grep "dak 9 a" /etc/dfsc.dat
A: 0 13000b1 59 17 0 b ** /dev/disk/ dsk 9 a
A: 0 13000b2 59 17 0 c ** /dev/rdisk/ dsk 9 a
```

Or try:

```
# awk '/dsk 9 / { print $4 }' </etc/dfsc.dat | uniq
59
```

We printed for the 4th field because it is HWID (see section 7.3). Also, be very careful with the search string; make sure the pattern is: /dsk<space><instance number><space>/ The <space> characters are very important.

The HWID is 59, and this is the one we need to remove from the files. Now that we have the HWID, we can remove it from the dfsl.dat and dfsc.dat files. We will do this using an undocumented switch "-Z" to the dsfmgx command.

```
# dsfmgx -Z rm_hwid 59 0
-dsk9a -dsk9b -dsk9c -dsk9d -dsk9e -dsk9f -dsk9g -dsk9h -dsk9a -dsk9b -dsk9c -dsk9d -dsk9e -dsk9f -dsk9g -dsk9h
```

This will remove the HWID entries from the dfsc.dat and dfsl.dat database files. Alternatively, if you need to remove entries from only one file, you can use the "rm_local_hwid" flag to remove the HWID from the dfsl.dat file or the "rm_cluster_hwid" flag to remove the HWID from the dfsc.dat file.

At this point, the "dsfmgx -m" command should work.