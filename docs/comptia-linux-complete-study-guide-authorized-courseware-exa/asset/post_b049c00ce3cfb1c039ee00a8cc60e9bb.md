
## 103.3 Perform basic file management

- Copy, move and remove files and directories individually
- Copy multiple files and directories recursively
- Remove files and directories recursively
- Use simple and advanced wildcard specifications in commands
- Using find to locate and act on files based on type, size, or time
- Usage of tar, cpio, and dd

The following is a partial list of the used files, terms and utilities:
- cat
- cut
- expand
- fmt
- head
- od
- join
- nl
- paste
- pr
- sed
- sort
- split
- tail
- tr
- unexpand
- uniq
- wc
- cp
- find
- mkdir
- mv
- ls
- rm
- rmdir
- touch
- tar
- cpio
- dd
- file
- gzip
- gunzip
- bzip2
- file globbing

## 103.4 Use streams, pipes and redirects

- Redirecting standard input, standard output and standard error
- Pipe the output of one command to the input of another command
- Use the output of one command as arguments to another command
- Send output to both stdout and a file

The following is a partial list of the used files, terms and utilities:
- tee
- xargs

## 103.5 Create, monitor and kill processes

- Run jobs in the foreground and background
- Signal a program to continue running after logout
- Monitor active processes
- Select and sort processes for display
- Send signals to processes

The following is a partial list of the used files, terms and utilities:
- &
- bg
- fg
- jobs
- kill
- nohup
- ps
- top
- free
- uptime
- killall

## 103.6 Modify process execution priorities

- Know the default priority of a job that is created
- Run a program with higher or lower priority than the default
- Change the priority of a running process

The following is a partial list of the used files, terms and utilities:
- nice
- ps
- renice
- top

## 103.7 Search text files using regular expressions

- Create simple regular expressions containing several notational elements
- Use regular expression tools to perform searches through a filesystem or file content

The following is a partial list of the used files, terms and utilities:
- grep
- egrep
- fgrep
- sed
- *regex(7)*

## 103.8 Perform basic file editing operations using vi

- Navigate a document using vi
- Use basic vi modes
- Insert, edit, delete, copy and find text

The following is a partial list of the used files, terms and utilities:
- vi
- `i, ?`
- `h,j,k,l`
- `i, o, a`
- `c, d, p, y, dd, yy`
- `ZZ, :w!, :q!, :e!`

# 104 Devices, Linux Filesystems, Filesystem Hierarchy Standard

## 104.1 Create partitions and filesystems

- Use various mkfs commands to set up partitions and create various filesystems such as:
    - ext2
    - ext3
    - xfs
    - reiserfs v3
    - vfat

The following is a partial list of the used files, terms and utilities:
- fdisk
- mkfs
- mkswap

## 104.2 Maintain the integrity of filesystems

- Verify the integrity of filesystems
- Monitor free space and inodes
- Repair simple filesystem problems

The following is a partial list of the used files, terms and utilities:
- du
- df
- fsck
- e2fsck
- mke2fs
- debugfs
- dumpe2fs
- tune2fs
- xfs tools (such as xfs_metadump and xfs_info)

## 104.3 Control mounting and unmounting of filesystems

- Manually mount and unmount filesystems
- Configure filesystem mounting on bootup
- Configure user mountable removableable filesystems

The following is a partial list of the used files, terms and utilities:
- /etc/fstab
- /media
- mount
- umount

## 104.4 Manage disk quotas

- Set up a disk quota for a filesystem
- Edit, check and generate user quota reports

The following is a partial list of the used files, terms and utilities:
- quota
- edquota
- repquota
- quotaon

## 104.5 Manage file permissions and ownership

- Manage access permissions on regular and special files as well as directories
- Use access modes such as suid, sgid and the sticky bit to maintain security
- Know how to change the file creation mask
- Use the group field to grant file access to group members

The following is a partial list of the used files, terms and utilities:
- chmod
- umask
- chown
- chgrp

## 104.6 Create and change hard and symbolic links

- Create links
- Identify hard and/or softlinks
- Copying versus linking files
- Use links to support system administration tasks

The following is a partial list of the used files, terms and utilities:
- ln

## 104.7 Find system files and place files in the correct location

- Understand the correct locations of files under the FHS
- Find files and commands on a Linux system
- Know the location and propose of important file and directories as defined in the FHS

The following is a partial list of the used files, terms and utilities:
- find
- locate
- updatedb
- whereis
- which
- type
- /etc/updatedb.conf

# LX0-102

The following are the areas (or *domains* according to CompTIA) in which you must be proficient in order to pass LX0-102

| Domain | Weight |
| :--- | :--- |
| 105 Shells, Scripting and Data Management | 17% |
| 106 User Interfaces and Desktops | 8% |
| 107 Administrative Tasks | 20% |
| 108 Essential System Services | 17% |
| 109 Networking Fundamentals | 23% |
| 110 Security | 15% |

# 105 Shells, Scripting and Data Management

## 105.1 Customize and use the shell environment

- Set environment variables (e.g. PATH) at login or when spawning a new shell
- Write BASH functions for frequently used sequences of commands
- Maintain skeloton directories for new user accounts
- Set command search path with the proper directory

The following is a partial list of the used files, terms, and utilities:
- /etc/profile
- env
- export
- set
- unset
- ~/bash_profile
- ~/.bash_login
- ~/profile
- ~/.bashrc
- ~/.bash_logout
- function
- alias
- lists

## 105.2 Customize or write simple scripts

- Use standard sh syntax (loops, tests)
- Use command substitution
- Test return values for success or failure or other information provided by a command
- Perform conditional mailing to the superuser
- Correctly select the script interpreter through the shebang (#!/) line
- Manage the location, ownership, execution and suid-rights of scripts

The following is a partial list of the used files, terms, and utilities:
- for
- while
- test
- if
- read
- seq

## 105.3 SQL data management

- Use of basic SQL commands
- Perform basic data manipulation

The following is a partial list of the used files, terms, and utilities:
- insert
- update
- select
- delete
- from
- where
- group by
- order by
- join

# 106 User Interfaces and Desktops

## 106.1 Install and configure X11

- Verify that the video card and monitor are supported by an X server
- Awareness of the X font server
- Basic understanding and knowledge of the X Window configuration file

The following is a partial list of the used files, terms, and utilities:
- `/etc/X11/xorg.conf`
- xhost
- DISPLAY
- xwininfo
- xdpyinfo
- X

## 106.2 Setup a display manager

- Turn the display manager on or off
- Change the display manager greeting
- Change default color depth for the display manager
- Configure display managers for use by X-stations

The following is a partial list of the used files, terms, and utilities:
- `/etc/inittab`
- xdm configuration files
- kdm configuration files
- gdm configuration files

## 106.3 Accessibility

- Keyboard Accessibility Settings (AccessX?)
- Visual Settings and Themes
- Assistive Technology (ATs)
