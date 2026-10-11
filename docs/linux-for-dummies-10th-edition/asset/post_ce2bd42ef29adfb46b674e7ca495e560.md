
## Archiving and Compressing

| TABLE A-1 Shell Help Commands |  |
| --- | --- |
| Command | Purpose |
| apropos | Looks for commands that contain a keyword in their man page descriptions. |
| info | One way of finding help information. You can find instructions for this tool at www.gnu.org/software/texinfo/manual/info-std/info-std.html, or you can use the built-in tutorial by starting the info tool and pressing the H key when inside it. |
| man | The primary way of getting help in Linux and UNIX. |
| whatis | Gets a one-line description of a command. |

Locating details about the command-prompt options of a command is a never-ending pursuit. The man page system provides some helpful guides at your fingertips for rapidly finding this detailed information.

Although disk space isn't as much of a premium as it once was, bandwidth and backup media still are. Subsequently, this group provides a potpourri of tools for compacting and organizing data for storage, as shown in Table A-2.

### Archiving and Compressing Tools

| Command | Purpose |
| --- | --- |
| bzip2 | Compresses files into .bz2 format. Used mostly for incredibly large sets of text files (which is what source code actually is). |
| bunzip2 | Uncompresses .bz2 files. |
| compress | Compresses files into .Z format. Pretty old and not used much in the Linux world. |
| gunzip | Uncompresses .gz files and .tgz files. |
| gzip | Compresses files into .gz format. |
| tar | Packages files together in a group. The most common way of using this command is `tar xvf filename`, such as `tar xvf download.tar`. |
| uncompress | Uncompresses files from .Z format. |
| unzip | Uncompresses files from .zip format. |
| xz | Compress and uncompress files from .xz format. |
| zip | Compresses files into .zip format. |

## Built-in bash commands

Some commands don't even seem to exist if you try to look up their help information in the `man` pages, and the commands don't show up as files on your system. Remember, as you type commands at the prompt, that you're communicating with a type of program called a `shell`. (In my case, it's `bash`, the default Linux shell.) The shell has a set of commands, included in the following list, that you can use to communicate with it, as shown in Table A-3.

### Shell Commands

| Command | Purpose |
| --- | --- |
| alias | Creates or lists command shortcuts. |
| env | Lists your current environment variables and their settings. |
| export | Whenever you're told to set an environment variable, create the variable and then use this command so that the variable will be remembered properly. |
| history | Lists off the last 1,000 commands you've typed. |
| unalias | Removes command shortcuts. |

If you try to view the `man` page entry for some of these commands, you find instead the help information for `BASH BUILTINS` loads. To search through this manual, press the forward slash (/) key to open the `man` search interface and then type the name of the command you want to search for. Press `Enter` to start the search. The interface stops in the first spot where the term is found. If you want to try again, press the `N` key to proceed to the next occurrence of the word.

For example, you might be reading the massive `bash` `man` page (`type` `man bash` to access this page), but perhaps you're only interested in items related to `prompts`, which are the bits of text that appear to the left of your cursor in a text window. An example prompt is

```
rich@testbox:~$
```

So, you might type `/prompt` and press `Enter` to jump down to the first instance of this word. If the text around the word doesn't reflect what you're looking for, press the `N` key to jump to the next one, and so on.

## Files and Filesystem

No matter which operating system you're using, it's hard to do anything without being able to find your way through and work with the filesystem. The following utilities help you find your way.

### File organization

Boxing, packing, sorting, shipping — I'm always shuffling files around on my system. File organization commands provide tools for moving files and filesystem units around, as shown in Table A-4.

#### File Organization Tools

| Command | Purpose |
| --- | --- |
| cd | Changes directories. |
| cp | Copies a file. |
| df | Shows partitions and how much space they have. |
| du | Shows how much disk is being used in the current directory and below. |
| ln | Creates a shortcut. |
| ls | Lists the contents of a directory or information about a file. |
| mkdir | Creates a directory. |
| mv | Moves or renames a file. |
| pwd | Shows the path for the directory you're currently in. |
| rm | Deletes a file. |
| rmdir | Deletes an empty directory. |

### File attributes

Files are much like candy bars. The wrappers provide information about the ingredients, size, and package date — all descriptive of the tasty nugget inside. (Perhaps the wrapper is even childproof.) Files keep all this wrapper information in an inode. Along with the capability to change file inode information, these commands can return data about the content of the file, as shown in Table A-5.

#### File Attributes Commands

| Command | Purpose |
| --- | --- |
| chgrp | Changes the group associated with a file. |
| chmod | Changes a file's permissions. |
| chown | Changes who owns a file. |
| file | Shows what type of file you're dealing with. |
| stat | Shows some statistics about the file. |
| touch | Creates an empty file of this name. |
| wc | Shows how many words, lines, and so on are in this file. |

### File locators

Where, oh, where can my file be? These commands, shown in Table A-6, help you locate files in Linux’s monster tree-structure filesystem.

#### File Locator Commands

| Command | Purpose |
| --- | --- |
| find | Hard-core filesystem search tool. |
| locate | Lighter-weight filesystem search tool. |
| which | Tells you the path for the program that would be run if you typed this command. |

### File viewers

Text file browsing is a favorite pastime of many a system user. These tools provide a variety of utilities for viewing the contents of readable text files of all sizes. Unlike using a full-screen editor, you cannot damage the contents of a file with these commands, shown in Table A-7, because they’re just viewers, not editors.

#### File Viewers

| Command | Purpose |
| --- | --- |
| cat | Dumps the contents of the file to your screen. |
| head | Shows the first ten lines of a file. |
| less | Shows the file a screen at a time, forward and backward. |
| more | Shows the file a screen at a time, forward only. |
| tail | Shows the last ten lines of a file. |

### Filesystem commands

These commands, listed in Table A-8, provide information or perform actions on the entire filesystem, from creation and tuning to repair and recovery. Some of these commands return data only, whereas others also provide you with surgical instruments for serious filesystem hacking.

#### Filesystem Commands

| Command | Purpose |
| --- | --- |
| badblocks | Searches a partition for bad blocks. |
| e2fsck | Checks and repairs an ext2 or ext3 filesystem. |
| e2label | Applies a filesystem label to an ext2 or ext3 partition. |
| eject | Ejects a CD or DVD. |
| fsck | Can check and repair many types of filesystems. |
| mkfs | Creates a filesystem (format a partition). |
| mount | Loads a partition into your filesystem. |
| sync | Saves all information out of buffers onto disks. |
| tune2fs | Adjusts ext2 and ext3 filesystem parameters. |
| umount | Removes a partition from the filesystem. |

## System Control

These commands provide systemwide information and control. Normal users can run many commands to obtain system information; however, commands that actively change the configuration of the system need to run while you’re logged in as root—or have utilized the `su` command to temporarily become the superuser.

### Administration

Some administration commands, shown in Table A-9, don’t fall neatly into a category.

#### Administration Commands

| Command | Purpose |
| --- | --- |
| passwd | Change a particular user’s password. Any user can run this command to change their own password. Only root can use it to change someone else’s. |
| su | Switch to another user account without logging out of this one. The best way to use this command is `su -` so your filesystem path and other information is loaded. |

### Kernel module handling

You may sometimes need to add kernel support for an additional device (software or hardware). If this need arises, you have a limited number of choices: You can either rebuild the kernel or install a loadable kernel module. Although rebuilding a kernel doesn’t exactly require a PhD in nuclear science, consider it a time-consuming nuisance that’s best to avoid. The commands in Table A-10 enable you to include the kernel support you need while the system is running, without having to rebuild the entire thing from scratch.

#### Kernel Support Commands

| Command | Purpose |
| --- | --- |
| depmod | Regenerates your module dependencies. |
| insmod | Loads a module by hand. |
| lsmod | Lists the modules your kernel has loaded. |
| modprobe | Loads a module by hand along with its dependencies and settings. |
| rmmod | Unloads a module by hand. |
