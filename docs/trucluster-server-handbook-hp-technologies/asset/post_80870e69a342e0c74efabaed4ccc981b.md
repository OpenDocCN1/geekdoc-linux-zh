
```shell
# clu_get_info | grep disk
Quorum disk : sdb4
```

- Check the device's disk label using the `disklabel(8)` command to see which partitions are unused and whether or not the partition you have in mind overlaps an “in use” partition.

```text
# disklabel sdb | grep -E "8 part"
8 partitions:
  size        offset    fstype  fsize  bsize  cpg  # cyl  values
 a:  2933672         0    4.2BSD   1024   8192   16  #  0 - 385*
 b:  3490644    1293637    unused      0      0    #  385* - 1557*
 c:  1773524         0    unused      0      0    #  0 - 5289*
 d:  3389144    5234331    unused      0      0    #  1557* - 2566*
 e:  4180140    8623475    unused      0      0    #  2566* - 3810*
 f:  4969099   12893615    unused      0      0    #  3810* - 5289*
 g:  5959156     5234331    unused      0      0    #  1557* - 3331*
 h:  6580037   11193487    unused      0      0    #  3331* - 5289*
```

- Check the /etc/fdmns subdirectories. These subdirectories contain symbolic links to the devices used by the AdvFS domains on the cluster. Do you remember the `fln` Korn shell function we created in chapter 6? If not, you can use an `ls(1)` command piped into the `awk(1)` command for this example or turn to chapter 6 and check it out.

```shell
# ls -l /etc/fdmns/* | sort | uniq

dsk0a -> /dev/disk/dsk0a
dsk0g -> /dev/disk/dsk0g
dsk1a -> /dev/disk/dsk1a
dsk1g -> /dev/disk/dsk1g
dsk1h -> /dev/disk/dsk1h
dsk2a -> /dev/disk/dsk2a
dsk6c -> /dev/disk/dsk6c
dsk7a -> /dev/disk/dsk7a
dsk7g -> /dev/disk/dsk7g
dsk7h -> /dev/disk/dsk7h
dsk8a -> /dev/disk/dsk8a
dsk8h -> /dev/disk/dsk8h
```

The equivalent ls and awk commands are:

```shell
# ls -l /etc/fdmns/* | awk '{ print $9,$10,$11 }' | sort | uniq
```

or:

```shell
# ls -lR /etc/fdmns | awk '/->/ { print $9,$10,$11 }' | sort
```

2. On one member in the cluster, run the `volsetup(8)` command.

```text
[imolar]
# volsetup dsk5h

LSM: Creating Logical Storage Manager device special files.
Checking for an existing LSM configuration

Initialize vold to the root disk group:
Add disk dsk5h to the root disk group as dsk5h:
Addition of disk dsk5h as dsk5h succeeded.
Initialization of vold and the root disk group was successful.
Volwatch daemon started - mail only

You must run 'volsetup -s' on each additional node in the
cluster to initially set up LSM, unless using the clu_add_member
to add additional nodes now. The clu_add_member utility
will automatically start LSM on the new node.
```

3. On all other existing members, run the `volsetup` command with the `-s` switch.

```text
[sheridan]
# volsetup -s

Starting LSM...
LSM: Creating Logical Storage Manager device special files.
LSM volwatch Service started - mail only
```

The `-s` switch is used to update the member’s `/etc/inittab` file, create member-specific LSM devices, and start the LSM daemons on the member.

> **NOTE:**
>
> If we had not already added the second member to the cluster with the `clu_add_member(8)` command, then step 3 would have been unnecessary because any new member added to the cluster, now that LSM is configured, will be automatically configured to use LSM. You will not need to use the `volsetup -s` command for any newly added members, only existing members.

## 14.5 LSM Commands

While the intent of this chapter is not to teach you how to use LSM, but rather to show you what the differences are between LSM on a standalone system and LSM in a cluster, we thought at least to give you an idea of which commands can be used to create LSM volumes.

LSM has a whole slew of commands that accomplish various tasks. Let’s look at which commands are used and when you may want to use them.

There are three interfaces that can be used with LSM:

- Graphical User Interface (GUI)⁴
- Menu-Based
- Command-line

There are two approaches that can be taken when working with LSM:

- Top-Down
- Bottom-Up

We’re not referring to driving down the highway with the “top down” or chugging a beer (“bottoms up!”) but rather how the commands are used to create and manipulate the various LSM components. Figure 14-7 illustrates the two approaches.

![](img/a0df85c2e542a8d6c913113908553aa4_365_0.png)

Figure 14-7: Top-Down vs. Bottom-Up

⁴ Requires the LSM-OA license PAK to use.
