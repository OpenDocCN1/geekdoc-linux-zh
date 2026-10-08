The **amdump** command performs requested backups; it is not designed for interactive use. For an interactive backup, you would use an archive tool like **tar** directly. The **amdump** is placed within a cron instruction to be run at a specified time. If, for some reason, **amdump** cannot save all its data to the backup medium (tape or disk), it will retain the data on the holding disk. The data can then later be directly written with the with the **amflush** command.

You can restore particular files as well as complete systems with the **amrestore** command. With the **amrecover** tool, you can select from a list of backups.

# ## Amanda Configuration

Configuration files are placed in /etc/amanda, and log and database files in /var/lib/amanda. These are created automatically on Fedora when you install the Amanda RPM package. You will also need to create a directory to use as a holding disk where backups are kept before writing to the tape. This should be on a file system with very large available space, enough to hold the backup of your largest entire host.

# ### /etc/amanda

Within the /etc/amanda directory are subdirectories for the different kind of backups you want to perform. Each directory will contain its own **amanda.conf** and **disklis** file. By default a daily backup directory is created called **DailySet1**, with a default **amanda.conf** and a sample **disklis** file. To use them, you will have to edit them to enter your system's own settings. For a different backup configuration, you can create a new directory and copy the DailySet1 amanda.conf and disklis files to it, editing them as appropriate. When you issue Amanda commands like **amdump** to perform backups, you will use the name of the /etc/amanda subdirectory to indicate the kind of backup you want performed.

```
amdump DailySet1
```

The /etc/amanda directory also contains a sample cron file, **crontab.sample**, that shows how a cron entry should look.

# #### amanda.conf

The **amanda.conf** file contains basic configuration parameters such as the tape type and logfile as well as holding file locations. In most cases you can just use the defaults as listed in the DailySet1/amanda.conf file. The file is commented in detail, telling you what entries you will have to change. You will need to set the tapedev entries to the tape device you use, and the tape type entry for your tape drive type. In the holding disk segment, you will need to specify the partition and the directory for the holding disk you want to use. See the amanda Man page and documentation for detailed information on various options.

# #### disklis

The **disklis** file is where you specify the file systems and partitions to be backed up. An entry lists the host, the partition, and the dump-type. The possible dump-types are defined in **amanda.conf**. The dump-types set certain parameters such as the priority of the backup and whether to use compression or not. The comp-root type will back up root partitions with compression and low priority, whereas the always-full type will back up an entire partition with no compression and the highest priority. You can define other dump-types in amanda.conf and use them for different partitions.