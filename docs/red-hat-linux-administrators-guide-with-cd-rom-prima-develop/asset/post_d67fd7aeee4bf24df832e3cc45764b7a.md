
You may be surprised that simply editing the file will not make the changes immediately. You must either log out and then log back in or call the file in question and have it reread its configuration. The best way to do this is to enter one of the following commands, depending upon what file you edited:

```
source /etc/profile
source ~/.bash_profile
```

The `~/` is referential to that user's own home directory. Rather than typing out the entire absolute path to your home directory, you can simply type a tilde and a forward slash.

The command `quotacheck` maintains the file system and debugs the level of user space consumption. This command should run when the computer boots up. Often this program is automatically set up with a default install. If not, then it should be set up as a cron job. Along with these commands are a series of related programs that check the system. The commands `quota` and `quotaoff` initialize the quota system for various file systems. The standard procedure for turning quotas on is as follows:

```
quotacheck -uv /home
```

Once quotas have been enabled, you can have the quota system report to you the total disk usage for all the file systems listed in `/etc/fstab`. The command `repquota -a` prints out the disk usage of the directories and users.

## Monitoring Disk Use

For less intensive monitoring of directories and simple reporting of disk usage, the command `du` accomplishes much the same thing. Depending upon your location and the directory that you are currently in, running `du` will show you the amount of hard drive space that each file occupies.

Again, because the output will probably exceed the number of lines that your terminal window can show, it is a good idea to pipe the result through the `more` and `less` commands. The `du` command checks not only your visible directories and files but also hidden file systems or those whose names are preceded by a period. Be forewarned that the output is extremely verbose and that you should implement some options if you want to see a limited result. You can also apply `du` to just one directory. Entering `du docs/ | more` prints out the size of each file found within that directory structure.

If the output appears too cryptic, try using some options such as `-k`, which then prints out the result in kilobytes. This gives a better real-world definition of space used. I prefer the `du -h` option, which prints out the end result in human readable format, in kilobytes and megabytes. Though the `-k` option is the default variable when displaying file sizes, some file systems might be set up differently. Using the `-a` option will also show you the file size of individual files and not just the directory sizes. This option is more verbose in its tabulating. You can consult the man page for `du` for additional information.

## Checking Partition Use

If you want to see the disk use for each partition, the command `df` is recommended. This command lists the amount of disk space consumed and the amount available for each partition. The `df` command can be viewed as the counterpart to the `du` command since `df` views the amount of space used and available for each partition whereas `du` examines directories.

The standard format for `df` is first to show the device name for each partition. The next few variables display how much space each partition can hold, the amount used, the remaining space available, and the percentage occupied by files. At the end of each line, the output shows the partition name assigned to the device name.

Like most commands, `df` takes different options so that you can refine the additional bits of information that the output displays. One of the most commonly used options is `-h`, which displays the output in a format that humans can understand—that is, in terms of kilobytes, megabytes, and gigabytes. In Listing 3.3, the default `df` command shows the space in terms of 1 kilobyte blocks. Listing 3.4 shows the `df` output with the `-h` option. Here the result is more understandable.

### Listing 3.3 A Sample Printout of Disk Use Showing Disk Space Consumption in Terms of 1 Kilobyte Blocks

```bash
$ df
```

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | 497829 | 38185 | 433942 | 8% | / |
| /dev/hda5 | 3470648 | 1230469 | 2060655 | 37% | /home |
| /dev/hda8 | 746387 | 378208 | 329625 | 53% | /opt |
| /dev/hda7 | 2016016 | 1341784 | 571820 | 70% | /usr |
| /dev/hda6 | 2478138 | 1563570 | 786452 | 67% | /usr/local |
| /dev/hda10 | 388693 | 34010 | 334604 | 9% | /var |

### Listing 3.4 A Printout of Disk Space in Terms of Megabyte Blocks

```bash
$ df -h
Filesystem   Size  Used Avail Use% Mounted on
/dev/hda1    486M  37M  424M   8% /
/dev/hda5    3.3G 1.2G  2.0G  37% /home
/dev/hda8    729M 369M  322M  53% /opt
/dev/hda7    1.9G 1.3G  558M  70% /usr
/dev/hda6    2.4G 1.5G  768M  67% /usr/local
/dev/hda10   380M  33M  327M   9% /var
```

Properly monitoring the amount of space used by each partition will help regulate the amount of space that can be allocated to each user. This also helps to prevent one partition from becoming overloaded. If you know that a partition is quickly approaching maximum capacity, you can take preventative action such as further reducing disk use, adding additional hard drives, or repartitioning existing drives. Knowledge of what your users are doing on your system is the key to keeping it operating at its optimal level.

## Conclusion

This chapter covered the most basic commands associated with viewing files and directories as well as moving and copying those files within differing locations. This chapter also highlighted how Red Hat Linux lays out certain file structures and what types of files each separate directory contains. You also learned what types of files exist under Linux and how you can modify file permissions and ownerships. Lastly, you examined how you can control and monitor the amount of disk space on a Linux drive.

This chapter covered the basics for initial navigation and preliminary system administration. It was designed for beginning users who need to understand how files function under the Linux operating system.

Once you have grasped the fundamentals of files and directories, including the setting of permissions for unique files, you can begin interacting with the command line. The next chapter will look at shells that allow the user to input additional commands to the system. Because Linux provides several different possible shells with which to operate, Chapter 4 will outline some of the advantages of each and provide examples of the pros and cons that each shell offers the average user.

# Chapter 4
Terminal Shells

The shell provides the interface between the user and the system. It is here that the user inputs commands, queries, or instructions. The shell is identified by either the prompt that appears at a console connection after logging in or the prompt that appears in any of the terminals via remote login or an X-Window session. There are different ways a shell can facilitate navigation and tasks under Linux. Though considered arcane by newer users, the shell still provides the most dynamic method of accessing and editing Linux files.

This chapter will cover the following topics:

- Examining the types of shells available
- Editing user files under the shell
- Creating shell scripts
- Customizing the shell prompt
- Understanding paths
- Specifying variables under the shell

## Prompts or Shells

Any experience that you have with Linux up to now has been in some type of shell or command-line interpreter. A *shell* can be identified by the prompt immediately preceding the input field under the command-line environment, but it is also much more. It is the entire program that enables you to navigate through the Linux structure and provides you with the means to send commands to the kernel and receive responses.

Like earlier versions of PCs, and UNIX machines, early Linux boxes enabled any user to type a particular command and have the system respond or perform an action. Users entered all these commands on the command line. These early versions involved nothing more than a bracket or `>`, after which users could input data. However, Linux has become, unlike DOS and some of the other text-only environments, extremely customizable. Under Linux there are several shells from
