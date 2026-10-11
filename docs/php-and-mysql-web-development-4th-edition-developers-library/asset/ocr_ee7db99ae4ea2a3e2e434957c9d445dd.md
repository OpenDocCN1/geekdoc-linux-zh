The server writes log files to the data directory by default, so a good precaution for securing your logs is to secure the data directory against being accessed on the server host by login accounts other than the one used by the MySQL administrator. For details of this procedure, see Section 13.1.2, "Securing Your MySQL Installation."

# ## 11.3 Relocating Data Directory Contents

Earlier parts of this chapter discuss the data directory structure in its default configuration, which is that all databases, status files, and log files are located within it. However, you have some latitude in determining the placement of the data directory's contents. MySQL enables you to relocate the data directory itself or certain elements within it. There are several reasons why you might want to do this:

+   - The filesystem that contains the data directory has become full and you need to move it to a filesystem with more capacity.
+   - If your data directory is on a busy disk drive, you can put it on a less active drive to balance disk activity across physical devices. You can put databases and log files on different drives or distribute databases across drives for the same reasons. Similarly, the InnoDB shared tablespace is conceptually a single large block of storage, but you can put its individual component files on different drives to improve performance. If you use partitioned tables, you can do the same with individual table partitions.
+   - Putting databases on one disk and logs on another disk helps minimize the damage that can be caused by a failure of a single disk.
+   - You might want to run multiple servers, each with its own data directory. This is one way to work around problems with per-process file descriptor limits, especially if you cannot reconfigure the kernel for your system to enable higher limits.

The rest of this section discusses which parts of the data directory can be moved and how you go about making such changes.

# ### 11.3.1 Relocation Methods

There are two ways to relocate the data directory or elements within it.

First, on any platform, you can specify an option at server startup, either on the command line or in an option file. For example, to specify the data directory location, start the server with a `--datadir=dir_name` option on the command line or put the following lines in an option file:

```
[mysqld]
datadir=dir_name
```

Typically, the option file group name for server options is `[mysqld]`, as shown in the example. However, depending on your circumstances, other option group names may be more appropriate. For example, the `[embedded]` group applies to the embedded server. If you're running multiple servers using `mysqld_multi`, the group names will be of the