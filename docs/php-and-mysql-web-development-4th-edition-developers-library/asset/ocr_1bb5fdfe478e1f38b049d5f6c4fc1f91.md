incrementally. The third format is similar, but includes a value indicating the maximum size to which the auto-extending file is allowed to grow. Only the final component of the tablespace may be listed as auto-extending.

The default auto-extend increment is 8 MB. To specify a different increment, set the `innodb_autoextend_increment` system variable.

# 12.7.3.1.2  Configuring the Shared InnoDB Tablespace

In the usual case, the shared tablespace consists only of regular files and does not include any raw partitions (device files). To perform the initial setup for a shared tablespace that contains only regular files, use this procedure:

+   1. Add the appropriate lines to the option file.
+   2. Make sure that the directories exist in which the tablespace component files are to be created. InnoDB creates files, but it will not create directories.
+   3. Make sure that none of the component files already exist.
+   4. Start the server. InnoDB will notice that the files do not exist, and will create and initialize them.

If you’ve already started the server without configuring InnoDB explicitly, InnoDB will have created a shared tablespace using the default configuration. To configure the tablespace explicitly, first stop the server and remove the InnoDB-related files (tablespace and log files). Then specify the configuration options you want to use and restart the server. (Do this *before* creating any InnoDB tables. Otherwise, you must dump the tables with `mysqldump` before reconfiguring and reload them afterward.)

It is a little more complex to use raw partitions as components of the InnoDB shared tablespace, but there are several reasons to consider doing so:

+   - You can easily create very large tablespaces. A partition component can span the entire extent of the partition, whereas regular file components are limited in size to the maximum file size allowed by your operating system.
+   - Raw partition files are guaranteed to be composed of entirely contiguous space on disk, whereas regular files are subject to filesystem fragmentation. When it initializes the tablespace, InnoDB tries to minimize fragmentation of regular files by writing enough zeros to the files to force space for them to be allocated all at once rather than incrementally. But this can only reduce fragmentation; it cannot guarantee that it will not occur.
+   - Raw partitions reduce overhead by eliminating the filesystem management layer. On some systems, this overhead may not be significant, but on others the difference might be enough to justify using partitions.

A factor that counts against using raw partitions in the InnoDB tablespace is that your system backup software might be oriented toward use with filesystems rather than partitions. In this case, using partitions would make it more difficult to perform system backups.