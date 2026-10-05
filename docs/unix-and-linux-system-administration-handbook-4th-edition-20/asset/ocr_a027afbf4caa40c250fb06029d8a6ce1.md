# Chapter 9

# Periodic Processes

The **-type f** argument is important because the Linux kernel source contains a directory called **core**. You wouldn't want to be deleting that, would you?

```
find / -xdev -atime +3 '-name '##' -o -name "*#" -o -name "*.-*" -o -name "*nfs*" -exec rm -f {} \;
```

This command deletes files that have not been accessed in three days and begin with . or # or nfs or ~ or .CKP. These patterns are typical of various sorts of temporary and editor backup files.

For performance reasons, some administrators use the **noatime** mount option to prevent the filesystem from maintaining access stamps. That configuration will confuse both of the **find** commands as the files will have been unregistered even if they were recently used. Unfortunately, the failure mode is to delete the files; be sure you are maintaining access times before using these commands as shown.

```
cd /tmp; find . -name *last+found -type d -mtime +3 -exec /bin/rm -f {} \;
```

This command removes all subdirectories of **/tmp** not modified in 72 hours. On most systems, plain files in **/tmp** are removed at boot by the system startup scripts. However, some systems do not remove directories. If a directory named **last+found** exists, it is treated specially and is not removed. This is important if /tmp is a separate filesystem. See page 260 for more information about **last+found**.

If you use any of these commands, make sure that users are aware of your cleanup policies before disaster strikes!

# Network distribution of configuration files

If you are running a network of machines, it's often convenient to maintain a network-wide version of configuration files such as the mail alias database. Usually, the relying sharing mechanism is some form of polling or periodic distribution, this is also an ideal task for cron. Master versions of system files can be distributed every with **rsync** or **rdist**.

Sometimes, postprocessing is required. For example, you might need to run the **newaliases** to convert a file of mail aliases to the hashed format using **sendmail.cf** because the **AutoRebuildAliases** option isn't in your **sendmail**. You might also need to load files into an administrative database such as NIS.

# Log file rotation

Systems vary in the quality of their default log management, and you will probably need to adjust the defaults to conform to your local policies. To "rotate