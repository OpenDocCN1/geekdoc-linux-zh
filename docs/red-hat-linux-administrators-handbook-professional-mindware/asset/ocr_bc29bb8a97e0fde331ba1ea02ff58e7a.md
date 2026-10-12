# ## Installing disk quota software

The official Red Hat CD-ROM comes with quota software. For example, to install the quota software for an x86 machine, run the following command from the CD-ROM's /RedHat/RPMS directory:

```
```bash
rpm -ivh quota-version.i386.rpm
```
```

After the quota software is installed, you are ready to configure it.

# ## Configuring your system to support disk quotas

First, decide which partitions you want to bring under disk quotas. Typically, these are the partition(s) for user home directories and Web space. Also, decide whether you want to enforce quotas per user, per group, or both. This discussion assumes that you want to enable disk quotas for the /home and /www partitions and want to enforce only the per-user disk quota for the /home partition and the per-group disk quota for the /www partition. It also assumes that you have an /etc/fstab file that looks like the following:

```
```
/dev/sda1  /home   ext2  defaults   1 2
/dev/sda5  /www    ext2  defaults   1 2
```
```

To enforce user-level disk quotas on /home, modify the first line as follows:

```
```
/dev/sda1  /home   ext2  defaults,usrquota  1 2
```
```

The new option in the mount option field in the preceding fstab line is needed to enable disk quotas for users. Similarly, to enable group-level disk quotas on /www, modify the second fstab line as follows:

```
```
/dev/sda5  /www    ext2  defaults,grpquota  1 2
```
```

Tip

You can also use both usrquota and grpquota for a single partition if you plan to enforce quotas for both users and groups.