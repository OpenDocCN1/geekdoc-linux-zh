
## Running quotacheck to Enable Quotas

After you have reconfigured and remounted the partitions, you have to tell Red Hat Linux to initialize the database files, examine the file system for usage, and turn on quotas. Use the **quotacheck** command to perform all these actions:

```
[root@tedford /root]# quotacheck -avug
```

The **-avug** options tell **quotacheck** to run on all file systems with quotas enabled, with verbose output so you know what it’s doing, and for both user- and group-based quotas.

![](img/ec2066d370d3af1a767664d36aa7ddfe_242_0.png)

> Red Hat recommends rerunning the **quotacheck** command periodically. You can do this by running a “cron” job on a weekly basis (see Module 8 for more about cron jobs).

## Configuring Quota Settings

Creating, modifying, and removing quotas on either a per-user or per-group basis is done via the **edquota** command. In this section, you’ll look at the usage of this command and run through some examples as well. First, some terminology:

- **Soft Limit**
  This requested limit is placed on a user or group. If the user’s account exceeds the soft limit, a grace period can be imposed as to how long the account can exist over the soft limit. During this time phase, users can be warned that their accounts are over the limit.
- **Hard Limit**
  This limit is imposed by the operating system and cannot be overrun. Any attempts to write data beyond the hard limit are denied.
- **Grace Period (Time Limit)**
  When a user’s account exceeds the soft limit, a clock starts tracking. After the grace period expires, the user cannot access the account. The length of this grace period should depend on the environment. A common value is one week. To keep the account from being disabled, the user needs to remove or compress files until his or her disk consumption falls below the soft limit.

### Command-Line Options of edquota

The **edquota** command has only three options when used to manage per-user quotas:

| Option | Description |
| :--- | :--- |
| `-u login` | Sets the quota information for the named user. |
| `-t` | Sets the grace period of a partition. Use it in conjunction with `-u` or `-g` to set all the grace periods for users or groups, respectively. Note: If users/groups exist on the same partition, they cannot have different grace periods. |
| `-g group` | Sets the *quota* information for the named *group*. |
| `-p login` | Allows you to clone one user’s (user *login*) information to another user. Must be set in conjunction with the `-u` option. |

When you invoke the edquota command, it brings up the configuration information for the particular user, group, or grace period you want to add or edit. By default, the vi editor is used to display human-readable information. If you prefer another editor, such as emacs or pico, you can simply change the EDITOR environment variable before running edquota. For example, if you’re using BASH (the root user’s default shell), you would enter this command:

```
[root@tedford]# export EDITOR=pico
```

Once the edquota information is on screen, you can edit it, save the document, and quit. The edquota process takes that information and places it into the database. Note that edquota uses the /etc/passwd file to determine the location of a user’s home directory.

### Examples of edquota

To place a quota on user blee, I would use the following command:

```
[root@tedford]# edquota -u blee
```

This will bring up the editor with a file that looks like the following:

> Quotas for user blee:
> /dev/hda2: blocks in use: 0, limits (soft = 0, hard = 0)
> inodes in use: 0, limits (soft = 0, hard = 0)

Zeros in all the limits means there is no quota on blee’s account at the moment. Notice that there is a limit value for i-nodes as well as blocks. Remember that one block is equal to 1K under Linux, and i-nodes are the control information needed to store files. You will usually need only a few i-nodes per file, and more as the file grows larger.

So to set blee’s soft block limit to 5000, the hard block limit to 6000, the soft i-node limit to 2500, and the hard i-node limit to 3000, I would edit the file to look like this:

> Quotas for user blee:
> /dev/hda2: blocks in use: 0, limits (soft = 5000, hard = 6000)
> inodes in use: 0, limits (soft = 2500, hard = 3000)

![](img/ec2066d370d3af1a767664d36aa7ddfe_243_0.png)

The edquota command generates a unique name for the temporary file used to edit this information. Keep this file—do not write over the quota.user or quota.group file with this information! The edquota utility will take care of integrating quota information into those two files for you.

To change the quota for **blee**, rerun `edquota -u blee` and change the limits.

Another example of using `edquota` is to clone one user’s settings to apply to another user. For example, if you want to clone the user **dalbers** so that user **dedood** gets the same quota values, you would enter this command:

```
[root@tedford]# edquota -p dalbers dedood
```

Here’s one more example: To apply quota settings to a large number of users at once, you can use a little one-line script to do it. Let’s assume that all of the affected users have their UIDs at greater than (or equal to) 500, and that at least one user has had his or her quota set up manually. For our example, we’ll call this user **arte**. The magic line is

```
[root@tedford]# edquota -p arte `awk -F ': $3 >> 499 print $1' /etc/passwd`
```

## Managing Quotas

Once you have your quotas enabled and working, there are three tools available to help you manage things: **quotacheck**, **repquota**, and **quota**.

### The quotacheck Command

The **quotacheck** command verifies the integrity of the quota database. In the script presented earlier for turning on the quota subsystem, you started by running this script with the **-avug** option set.

The options you can pass to **quotacheck** are as follows:

| Option | Description |
| :--- | :--- |
| `-v` | Turns on verbose mode. This presents useful and interesting information as the quota databases are checked. |
| `-u uid` | Checks the allocation of the user whose UID is *uid*. |
| `-g gid` | Checks the allocation of all users whose GID is *gid*. |
| `-a` | Checks all file systems that have quotas (as determined by the /etc/fstab file). |
| `-r` | Used in conjunction with `-a`. Checks all partitions with quotas, except the root partition. |

### The repquota Command

The **repquota** command generates a summary report of quota usage on the system. This command takes the following options:

| Option | Description |
| :--- | :--- |
| `-a` | Reports on all file systems. |
| `-v` | Reports on all quotas, even if there is no usage. |
| `-g` | Reports on quotas for groups only. |
| `-u` | Reports on quotas for users only. |

### The quota Command

Finally, the `quota` command is for users. It allows them to view the quota limitations placed on them. It takes the following options:

| Option | Description |
| :--- | :--- |
| `-g` | Prints quotas on groups of which the user is a member. |
| `-u` | Prints quota information about the specific user (default). |
| `-v` | Prints quota information as it pertains to the user for all file systems that support quotas. |
| `-q` | Prints a message to the user if he is over quota. |

For example, if user `rwhte` were to run `quota -v`, he would see this:

```
[rwhte@tedford ~]$ quota -v
Disk quotas for user rwhte (uid 500):
  File system blocks quota limit grace files quota limit grace
  /dev/hda8   0     0     0      0     0     0
  /dev/hdb1   0  5000  5100     0  1000  1100
```

## Project 7-2 Setting Up autofs

In this project, you’ll set up the autofs daemon and set quotas for a group of users. If you can configure your Red Hat Linux test system to be similar to the situation described, that will help, but if not, bend the details to fit your situation.

Consider the following situation: User `pddood` purchased the Linux system you’re managing (named tedford), and has several projects running on it. He also wants users `jwang`, `dalbers`, and `blee` to be able to use space on the system, but he doesn’t want them filling up his disk. The server, tedford, has a `/home` partition with 8GB of space. The other users already have accounts on tedford, and their Linux workstations can already mount `/home` via NFS, but the users complain that mounting tedford manually is difficult. Make everybody happy.

### Step by Step

1. The first step is to configure the disk quotas on tedford. There’s no sense in allowing the users easy access until the necessary restrictions are in place. Enable group-based disk quotas on the server by editing the `/etc/fstab` file as described in this module.
2. Remount the partition and enable quotas on the system by running the `quotacheck` command with the appropriate options.
3. Configure the group quota using a suitable `edquota` command.
4. On each remote system, create an `/etc/auto.home` file to automount tedford’s `/home` partition in the remote system’s `/home` directory.
