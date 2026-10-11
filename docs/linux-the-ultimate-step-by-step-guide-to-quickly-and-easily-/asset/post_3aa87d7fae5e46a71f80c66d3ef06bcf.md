
## Using Multiple sed Commands

You can use multiple $sed$ commands in a single $sed$ command as follows:

```bash
$ sed -e 'command1' -e 'command2' ... -e 'commandN' files
```

Here $command_1$ through $command_N$ are $sed$ commands of the type discussed previously. These commands are applied to each line in the list of files given by `files`. Using the same mechanism, we can write the above phone number example as follows:

```bash
$ sed -e 's/^[[[:digit:]]{3}\]/(&)/g' \
-e 's/[[[:digit:]]{3}/&-/g' phone.txt

(555)555-1212
(555)555-1213
(555)555-1214
(666)555-1215
(666)555-1216
(777)555-1217
```

**Note** – In the above example, instead of repeating the character class keyword `[[digit:]]` three times, you replaced it with `\{3\}`, which means to match the preceding regular expression three times. Here I used `\` to give line break; you should remove this before running this command.

## Back References

The ampersand metacharacter is useful, but even more useful is the ability to define specific regions in a regular expression so you can reference them in your replacement strings. By defining specific parts of a regular expression, you can then refer back to those parts with a special reference character. To do back references, you have to first define a region and then refer back to that region. To define a region, you insert backslash parentheses around each region of interest. The first region that you surround with backslashes is then referenced by `\1`, the second region by `\2`, and so on.

Assuming `phone.txt` has the following text:

```text
(555)555-1212
(555)555-1213
(555)555-1214
(666)555-1215
(666)555-1216
(777)555-1217
```

Now try the following command:

```bash
$ cat phone.txt | sed 's/\^(.*)\(.*)\(.*)/Area \ code: \1 Second: \2 Third: \3/'

Area code: (555) Second: 555- Third: 1212
Area code: (555) Second: 555- Third: 1213
Area code: (555) Second: 555- Third: 1214
Area code: (666) Second: 555- Third: 1215
Area code: (666) Second: 555- Third: 1216
Area code: (777) Second: 555- Third: 1217
```

**Note:** In the above example, each regular expression inside the parentheses would be back-referenced by `\1`, `\2`, and so on. Here I used `\` to give line break; you should remove this before running this command.

# Chapter Eighteen: FILE SYSTEM BASICS

A file system is a logical collection of files on a partition or disk. A partition is a container for information and can span an entire hard drive if desired. Your hard drive can have various partitions which usually contain only one file system, such as one file system housing the `/` file system or another containing the `/home` file system. One file system per partition allows for the logical maintenance and management of differing file systems. Everything in Unix is considered to be a file, including physical devices such as DVD-ROMs, USB devices, floppy drives, and so forth.

## Directory Structure

Unix uses a hierarchical file system structure, much like an upside-down tree, with root (`/`) at the base of the file system and all other directories spreading from there. A UNIX file system is a collection of files and directories that have the following properties:

- It has a root directory (`/`) that contains other files and directories.
- Each file or directory is uniquely identified by its name, the directory in which it resides, and a unique identifier, typically called an inode.
- By convention, the root directory has an inode number of 2 and the `lost+found` directory has an inode number of 3. Inode numbers 0 and 1 are not used. File inode numbers can be seen by specifying the `-i` option to the `ls` command.
- It is self-contained. There are no dependencies between one file system and any other.

The directories have specific purposes and generally hold the same types of information for easily locating files. The following are the directories that exist on the major versions of Unix:

| Directory | Description |
| :--- | :--- |
| / | This is the root directory, which should contain only the directories needed at the top level of the file structure. |
| /bin | This is where the executable files are located. They are available to all users. |
| /dev | These are device drivers. |
| /etc | Supervisor directory commands, configuration files, disk configuration files, valid user lists, groups, ethernet, hosts, where to send critical messages. |
| /lib | Contains shared library files and sometimes other kernel-related files. |
| /boot | Contains files for booting the system. |
| /home | Contains the home directory for users and other accounts. |
| /mnt | Used to mount other temporary file systems, such as cdrom and floppy for the CD-ROM drive and floppy diskette drive, respectively. |
| /proc | Contains all processes marked as a file by process number or other information that is dynamic to the system. |
| /tmp | Holds temporary files used between system boots. |
| /usr | Used for miscellaneous purposes, can be used by many users. Includes administrative commands, shared files, library files, and others. |
| /var | Typically contains variable-length files such as log and print files and other file types that may contain a variable amount of data. |
| /sbin | Contains binary (executable) files, usually for system administration. For example `fdisk` and `ifconfig` utilities. |
| /kernel | Contains kernel files. |

## Navigating the File System

Now that you understand the basics of the file system, you can begin navigating to the files you need. The following are commands you will use to navigate the system:

| Command | Description |
| :--- | :--- |
| `cat filename` | Displays a filename. |
| `cd dirname` | Moves you to the directory identified. |
| `cp file1 file2` | Copies one file/directory to specified location. |
| `file filename` | Identifies the file type (binary, text, etc). |
| `find filename dir` | Finds a file/directory. |
| `head filename` | Shows the beginning of a file. |
| `less filename` | Browses through a file from end or beginning. |
| `ls dirname` | Shows the contents of the directory specified. |
| `mkdir dirname` | Creates the specified directory. |
| `more filename` | Browses through a file from beginning to end. |
| `mv file1 file2` | Moves the location of or renames a file/directory. |
| `pwd` | Shows the current directory the user is in. |
| `rm filename` | Removes a file. |
| `rmdir dirname` | Removes a directory. |
| `tail filename` | Shows the end of a file. |
| `touch filename` | Creates a blank file or modifies an existing file's attributes. |
| `whereis filename` | Shows the location of a file. |
| `which filename` | Shows the location of a file if it is in your PATH. |

You can use **Manage Help** to check complete syntax for each of these commands.

## The df Command

The first way to manage your partition space is with the *df* (disk free) command. The command `df -k` (disk free) displays the disk space usage in kilobytes, as shown below:

```bash
$ df -k
Filesystem 1K-blocks Used Available Use% Mounted on
/dev/vzfs 10485760 7836644 2649116 75% /
/devices 0 0 0 0% /devices
$
```

Some of the directories, such as `/devices`, show 0 in the kbytes, used, and avail columns as well as 0% for capacity. These are special (or virtual) file systems, and although they reside on the disk under `/`, by themselves they do not take up disk space.

The `df -k` output is generally the same on all Unix systems. Here's what it usually includes:

| Column | Description |
| :--- | :--- |
| **Filesystem** | The physical file system name. |
| **Kbytes** | Total kilobytes of space available on the storage medium. |
| **Used** | Total kilobytes of space used (by files). |
| **Avail** | Total kilobytes available for use. |
| **Capacity** | Percentage of total space used by files. |
| **Mounted on** | What the file system is mounted on. |

You can use the `-h` (human readable) option to display the output in a format that shows the size in easier-to-understand notation.

## The du Command

The `du` (disk usage) command enables you to specify directories to show disk space usage on a particular directory. This command is helpful if you want to determine how much space a particular directory is using. The following command will display the number of blocks used by each directory. A single block may take either 512 Bytes or 1 Kilo Byte depending on your system.

```bash
$ du /etc
10	/etc/cron.d
126	/etc/default
6	/etc/dfs
...
$
```

The `-h` option makes the output easier to comprehend:

```bash
$ du -h /etc
5k	/etc/cron.d
63k	/etc/default
3k	/etc/dfs
...
$
```

## Mounting the File System

A file system must be mounted in order to be usable by the system. To see what is currently mounted (available for use) on your system, use this command:

```bash
$ mount
/dev/vzfs on / type reiserfs (rw,usrquota,grpquota)
proc on /proc type proc (rw,nodiratime)
devpts on /dev/pts type devpts (rw)
$
```
