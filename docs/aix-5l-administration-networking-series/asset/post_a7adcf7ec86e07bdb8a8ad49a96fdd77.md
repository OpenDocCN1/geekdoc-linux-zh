
Important in environments where users have accounts on multiple machines. Some examples include HACMP clusters (HACMP stands for High Availability Cluster Multi-Processing; see Chapter 28 for details); in distributed environments, or if you are using Network File System (NFS), you must ensure that UIDs are consistent across all of the systems. *By consistent*, I mean that if user “stimpoy” is UID 1234 on host A, then the same UID is reserved for stimpoy on any other system. Ownership and permission problems can arise if the same UID represents different users in clustered, distributed, and NFS environments. Remember, the operating system identifies users by UID, not by user name.

While you define your UID space, it’s also a good idea to plan your Group ID (GID) space. Groups provide a coarse mechanism for sharing information between users. File and directory permissions offer read, write, and execute permissions for world, group, and owner. AIX and other UNIX flavors assume a limited group set to implement access privileges. What needs to be decided is whether you want to implement other GID sets for specific workgroups or collaborators. If your user base is small, this can be done relatively easily. For large numbers of users, managing GID sets can be a big chore.

## The /etc/group and /etc/security/group Files

All GID mapping is maintained in the `/etc/group` and `/etc/security/group` files. The `/etc/group` file lists each group name and GID followed by the list of members, or user names. The `/etc/security/group` file contains a stanza for each group name in the `/etc/group` file, indicates whether the group may be administered by users other than root, and identifies the administrators by user name. Groups and their associated attributes are managed through SMIT or WebSM, or else from a series of group management commands listed here:

```text
mkgroup        - Create a new group
chgrp         - Change group attributes
lsgr          - List groups and attributes
chggrpm       - Change administrators or members of a group
setgrps       - Reset the current groups set for a user
newgrp        - Set the group ID for session
rmgr          - Remove a group
```

Now for a few examples. The first file is a sample `/etc/group`; the second file is a sample `/etc/security/group`.

### A Sample /etc/group File

```text
system::0:root,ops
daemon::1::
bin::2:root,bin
sys::3:root,bin,sys
adm::4:bin,adm,kenn,root
user:!:5:uucp
mail:!:6:
security:!:7:root
cron:!:8:root
staff:!:10:root,ren,stimpy,daffy,huey,dewey
user:!:30:luge,acadmus,gw9neira,bungi
```

### A Sample /etc/security/group File

```text
system:
     admin = true
daemon:
     admin = true
bin:
     admin = true
sys:
     admin = true
adm:
     admin = true
uucp:
     admin = true
mail:
     admin = true
security:
     admin = true
cron:
     admin = true
staff:
     admin = false
     adma = ren,stimpy
user:
     admin = false
```

## RESOURCE LIMITS

How much of the pie are you going to give each user? How do you make sure each user gets no more than his or her fair share? Profiling the application mix with estimated concurrent users will give you some ballpark figures. AIX provides the capability to enforce limits on each user's slice of the available system resources through operating system controls. Limits can be defined for CPU, memory, and disk utilization on a per-process basis. The total number of concurrent processes per user is capped by the kernel configuration parameter. Aggregate filesystem usage can be governed through activating disk quotas at user and group levels.

### The /etc/security/limits File

The kernel manages per-process limits using the `setrlimit()`, `getrlimit()`, and `vlimit()` system calls. Each process has an associated rlimit structure that indicates soft and hard ceilings for each resource type. The rlimit structure is defined in `/usr/include/sys/resource.h`. Default and resource limits for the system and users are specified in the `/etc/security/limits` file. Each user defined to the system is represented by a stanza identified by user name. System defaults are active for each user that does not have an overriding parameter under the user's stanza. When a process exceeds one of the specified limits, it is killed. Check out the sample `/etc/security/limits` file here:

#### A Sample /etc/security/limits File

```text
*
* Sizes are in multiples of 512 byte blocks, CPU time is in seconds
* fsize - soft file size in blocks
* core - soft core file size in blocks
* cpu - soft per process CPU time limit in seconds
* data - soft data segment size in blocks
* stack - soft stack segment size in blocks
* rss - soft real memory usage in blocks
* fsize_hard - hard file size in blocks
* core_hard - hard core file size in blocks
* cpu_hard - hard per process CPU time limit in seconds
* data_hard - hard data segment size in blocks
* stack_hard - hard stack segment size in blocks
* rss_hard - hard real memory usage in blocks
*
* The following table contains the default hard values if the
* hard values are not explicitly defined:
*
* Attribute       Value
* =========       =========
* fsize_hard      set to fsize
* cpu_hard        set to cpu
* core_hard       -1
* data_hard       -1
* stack_hard      -1
* rss_hard        -1
*
* NOTE: A value of -1 implies "unlimited"
*

default:
		fsize = 2097151
		core = 2048
		cpu = -1
		data = 262144
		rss = 65536
		stack = 65536

root:
daemon:
bin:
sys:
adm:
uucp:
guest:
nobody:
lpd:
stmpy:
		fsize_hard = 10240
		cpu_hard = 3600
muucp:
```

The kernel limits the maximum number of processes per user as specified by the kernel configuration parameter `maxproc`. The default value of 40 indicates that up to 40 processes may be running concurrently for a given user. The value may not be exceeded by logging into the system multiple times. The `maxproc` value may be altered using SMIT, WebSM, or the `chdev` command (see the SMIT panel in Figure 20-1).

```text
# chdev -l sys0 -a maxproc=80
# smit chgys
```

![](img/82f851021955589d82b22750fb3b1646_454_0.png)

**Figure 20-1.** Change / Show Characteristics of the Operating System SMIT panel

Disk quotas limit the maximum number of blocks a user or group may consume in quota-participating filesystems. The AIX implementation of disk quotas is based on BSD quotas. User and group quota limits are set by the Systems Administrator using the **edquota** command. Quota limits for disk blocks and i-nodes are specified by three parameters: soft limit, hard limit, and grace period. A user may exceed the soft limits for a default grace period of one week. When the grace period expires, the soft limits become hard limits.

The value of the soft limit indicates at what point the user or group begins receiving warnings that the soft limit has been exceeded, and that the hard limit is being approached. Warnings are delivered at login time and at each close that exceeds the specified limit. The hard limit specifies at what point the user or group will no longer be able to allocate additional disk space or i-nodes. The grace period defines a period of time that the user or group has to reduce utilization below the soft limit value. If utilization is not reduced before the grace period expires, the soft limit is enforced as a hard limit.

To implement disk quotas on a filesystem, use the **chfs** command to edit the stanza entry in */etc/filesystems* associated with the filesystem name. Add the parameter `quota=<userquota>,<groupquota>` to the stanza. The userquota and groupquota values indicate the quota types to be enforced. The quota limits for each user or group are recorded in files in the top-level directory named quota.user or quota.group, respectively. You may override these filenames with your own by including `userquota=<pathname>` and `groupquota=<pathname>` parameters in the filesystem stanza.

Add the stanza entries to /etc/filesystems with the following command:

```text
# chfs -a 'quota=userquota' -a 'userquota=/home1/user.quota' /home1
```

Check the /etc/filesystems stanza using the following **more** command:

```text
# more /etc/filesystems
/home1:
    dev = /dev/lv43
    vfs = jfs
    log = /dev/loglv00
    mount = true
    check = true
    options = rw
    quota = userquota
    userquota = /home1/user.quota
```

If the quota limit files do not exist in the filesystem, you can create them using **touch**.

```text
# touch /home1/quota.user
```

Use the edquota command to create a user quota for one of the users on the system. These values can be used as a template for setting the limits for other users on the system. The edquota command will invoke the default editor, specified by the EDITOR environment variable, and display the quota values for update.

```text
# edquota stimpys
Quotas for user stimpys:
/home1: blocks in use: 50, limits (soft = 80, hard = 100)
    inodes in use: 11, limits (soft = 120, hard = 150)
/home2: blocks in use: 0, limits (soft = 80, hard = 100)
    inodes in use: 0, limits (soft = 120, hard = 150)
```

After setting the soft and hard limits for the default user, invoke `edquota -p <default-user> <new-user>` to clone the default limits for each additional user in the system.

```text
# edquota -p stimpys ren
```
