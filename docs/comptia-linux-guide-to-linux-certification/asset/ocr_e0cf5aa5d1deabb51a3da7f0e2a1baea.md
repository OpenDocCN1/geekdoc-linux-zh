To view the status of the disks that are part of the datastorage3 pool, you can use the following command:

```
```shell
[root@server1 ~]# zpool status datastorage3
pool: datastorage3
state: DEGRADED

status: One or more devices could not be used because the label is missing or
        invalid. Sufficient replicas exist for the pool to continue func-
        tioning in a degraded state.
action: Replace the device using `zpool replace`.
see: http://zfsonlinux.org/msg/ZFS-8000-4J
scan: scrub repaired 0 in 0h0m with 0 errors on Tue Sep 30 13:33:11 2014
config:

		NAME			STATE	READ	WRITE	CKSUM
		datastorage3		DEGRADED	0	0	0
		mirror-0			DEGRADED	0	0	0
	/dev/sde			UNAVAIL	0	0	0 corrupted data
	/dev/sdf			ONLINE	0	0	0

errors: No known data errors
[root@server1 ~]# _
```
```

Notice from the preceding example that one of the disks in the mirror has failed (`/dev/sde`). In this case, you should detach the device from the pool using the `zpool detach datastorage3 /dev/sde` command, replace the failed hard disk, and reattach the disk to the mirror using the `zpool attach datastorage3 /dev/sdf /dev/sde` command. During this process, the filesystem is still available to users for reading and writing data. After reattaching the new hard disk, the output of the `zpool status datastorage3` command should resemble the following output:

```
```shell
[root@server1 ~]# zpool status datastorage3
pool: datastorage3
state: ONLINE
scan: none requested
config:

		NAME			STATE	READ	WRITE	CKSUM
		datastorage3		ONLINE	0	0	0
		mirror-0			ONLINE	0	0	0
	/dev/sde			ONLINE	0	0	0
	/dev/sdf			ONLINE	0	0	0

errors: No known data errors
[root@server1 ~]# _
```
```

To create ZFS pool and RAID-Z volume (the equivalent of a RAID-5 volume with a variable-sized stripe) called datastorage4 from the /dev/sdg, /dev/sdh, and /dev/sdi hard disks and mount it to /datastorage4, you simply need to specify the `raidz` keyword during creation, as shown here:

```
```shell
[root@server1 ~]# zpool create datastorage4 raidz /dev/sdg /dev/sdh /dev/sdi
[root@server1 ~]# _
```
```