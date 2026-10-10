# ## Checking a Filesystem for Errors

Creating partitions and file systems are tasks you're likely to perform every once in a while—say, when adding a new hard disk or making major changes to an installation. Another task is much more common: checking a file system for errors. Bugs, power failures, and mechanical problems can all cause the data structures on a file system to become corrupted. If these problems are left unchecked, they can cause severe data loss. For this reason, Linux includes tools for verifying a file system's integrity and for correcting any problems that might exist. The main tool you'll use for this purpose is called fsck. Like mkfs, fsck is actually a front-end to other tools, such as e2fsck (aka fsck.ext2 and fsck.ext3). The syntax for fsck is as follows:

```
fsck   [-sACVRTNP] [-t fstype] [--] [fsck-options]  filesystems
```

The more common parameters to this command enable you to perform useful actions, as summarized in Table 6.5.

### TABLE 6.5  fsck Options

| Option | Description |
| :--- | :--- |
| -A | This option causes fsck to check all the file systems marked for routine checks in /etc/fstab. This option is normally used in system startup scripts. |
| -C | This option displays a text-mode progress indicator of the check process. Most file system check programs don't support this feature, but e2fsck does. |
| -V | Verbose output can be produced by using this option. |
| -N | This option tells fsck to display what it would normally do, without actually doing it. |
| -t fstype | Normally, fsck determines the file system type automatically. You can force the type with this flag, though. If used in conjunction with -A, this causes the system to check only the specified file system types, even if others are marked to be checked. If fstype is prefixed with no, then all file systems except the specified type are checked. |
| Filesystem-specific options | File system check programs for specific file systems often have their own options. The fsck command passes options it doesn't understand, or those that follow a double dash (--), to the underlying check program. Common options include -a or -p (perform an automatic check), -r (perform an interactive check), and -f (force a full file system check even if the file system initially appears to be clean). |