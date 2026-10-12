
many files and directories of an operating system such as Red Hat Linux. The benefit of the FHS standard lies in compatibility with other FHS-compliant systems. For example, if a software developer wishes to support both Red Hat Linux and another FHS compliant Linux distribution, he or she can simply make the installation program use a standard directory for installing the software. This makes life easier for both developers and users of the software. The details of the FHS standard are available at www.pathname.com/fhs.

The top directories of a FHS system are shown in Table 8-1.

## Table 8-1 Top Directories of an FHS System

| Directory | Purpose |
|---|---|
| / | The root directory. |
| /bin | Contains essential command binaries. |
| /boot | Contains boot loader files. |
| /dev | Contains device files. |
| /etc | Contains system configuration files. |
| /lib | Contains kernel modules and shared library files. |
| /mnt | Usually used for storing mount point directories for removable media such as CD-ROM, floppy drive, etc. |
| /opt | Contains third-party applications. |
| /sbin | Contains system binaries. |
| /tmp | Temporary space for all users. |
| /usr | This is a separate directory structure of its own. It is discussed in Table 8-2. |
| /var | Variable data space used by programs to store logs, spools, etc. |

The /usr directory structure is very important because it is (usually) available throughout the entire file system for all users. The /usr directory structure is shown in Table 8-2.

## Table 8-2 The /usr Directory Structure

| Directory | What's in It |
|---|---|
| /usr/bin | User executable programs are kept here. |
| /usr/doc | Miscellaneous documentation for /usr/bin programs. |
| /usr/etc | Configuration files for programs in /usr/bin. |
| /usr/games | Silly games. |
| /usr/include | C header (include) files that are needed to compile other software. |
| /usr/kerberos | Kerberos authentication related binaries and other files. |
| /usr/lib | Library files that are required by many programs. |
| /usr/libexec | Small programs that are needed by many programs. |
| /usr/local | This directory is a hierarchy of its own. It is dedicated to locally compiled or developed programs. Usually it has the following subdirectories: /bin (for binaries), /doc (for documentation), /etc (for configuration), /lib (for library files), /src (for source code). |
| /usr/man | Online manual pages for many programs. |
| /usr/sbin | System administration programs. |
| /usr/share | Shared documentation and other files that are not architecture specific. |
| /usr/src | Source code for many programs in the /usr hierarchy. |
| /usr/X11R6 | X Window System-specific files and directories. |

## Accessing Files and Directories

This section shows you how to work with a few commonly used file and directory commands that are available on your Red Hat Linux system. You can access these commands from a shell prompt or an xterm session if you're using a GUI.

### Changing directories with cd

The cd command is really a built-in shell command. To use the cd command, simply run the command as follows, where directory is the name of the directory you want to change to:

```
cd directory
```

Note that if the directory you want to change to is not a subdirectory of your current working directory, you'll need to specify the full path to the directory. One exception to this is the cd .. command, which moves you up one directory.

![](img/9eb7e89292d2f85707b4d49102c865b7_195_0.png)

> If you don't provide a directory name as an argument, the cd command returns you to the home directory of the user account you are currently using. Any time you are in doubt about where you are in the file system, use the pwd command, which displays your current directory name.

### Listing files in a directory with ls

The ls program probably is the most widely used program on any Unix or Unix-like platform. ls is often used as a standalone command, with no options. However, you can customize the output of the ls command easily by using options. The most common options for ls are listed in Table 8-3.

## Table 8-3 Commonly Used ls Options

| Option | Purpose |
|---|---|
| -l | Long listing which shows the file permissions, last modification date and time, owner name, group name, etc. |
| -a | All files including filenames that start with a period (these are often called hidden dot files) |
| -1 | Single-column, filenames-only listing |
| -R | Recursive listing |

### Creating new directories with mkdir

Use the mkdir command to create new directories. The syntax of the mkdir command is mkdir new_directory_name. For example, to create a new directory called newsoftware, run the following command:

```
mkdir /newsoftware
```

If you want to create a directory path such as /dir1/dir2/dir3 in a single command, run a command like the following (replacing the names of the directories with your own):

```
mkdir -p /dir1/dir2/dir3
```

This creates all the three directories if they do not exist already.

### Finding files and directories

You can use various commands to locate a file. The following sections briefly discuss the more popular file-locating commands: which, locate, and find.

### Locating the path of a program with which

To locate the exact path of a program, use the which command. For example, the following command shows you the fully qualified path name of the httpd program if it is available in a directory that is included in the $PATH environment variable:

```
which httpd
```

![](img/9eb7e89292d2f85707b4d49102c865b7_196_0.png)

Some shells have a built-in which command, and others use /usr/sbin/which instead.

### Locating a file or directory with locate

You can locate a file or directory with a partial or full name using the locate program. For example, the following command queries the updatedb filename database and returns all occurrences of the netpr.pl file:

```
locate netpr.pl
```

![](img/9eb7e89292d2f85707b4d49102c865b7_196_1.png)

For locate to work properly, you must have a cron job set up to run updatedb on a daily basis so that the database is up to date when you query it. The default Red Hat installation sets up such a job automatically.

### Finding a file or directory with find

You can also use the find program to locate files or directories. For example, to locate all of the HTML files in the current directory and all of its sub-directories, run find as follows:

```
find . -type f -name "*.html"
```

## Accessing common removable devices

Files and directories that are stored in removable media such as CD-ROM or floppy drives can only be accessed after the device is mounted by the operating system. In this section I show you how to mount common devices such as CD-ROM or floppy drives and access their contents.

### Mounting a CD-ROM from the command line

Mounting a CD-ROM is quite simple. If you are working in a text mode environment (i.e., using a remote shell or console) you can do the following to mount a CD-ROM:

- 1. Insert a CD-ROM in the CD-ROM drive.
- 2. As root, run the mount /mnt/cdrom command to mount the CD-ROM. You should now be able to access the inserted CD-ROM from the /mnt/cdrom directory.

![](img/9eb7e89292d2f85707b4d49102c865b7_197_0.png)

The mount /mnt/cdrom command should work by default because Red Hat Linux comes with the following configuration line in the /etc/fstab file to mount CD-ROMs by using the above command.

```
/dev/cdrom /mnt/cdrom iso9660 noauto,owner,kudzu,ro 0 0
```

In case this command does not work for you, you can use mount -t iso9660 /mnt/cdrom /dev/cdrom command instead.

- 3. When you need to eject the CD-ROM, you should unmount it using `umount /mnt/cdrom` command and then run the `eject /mnt/cdrom` command to eject it.

### Mounting a CD-ROM from a graphical environment

If you're using the X Window System, you should be able to access the CD-ROM after you have inserted it in the CD-ROM drive. Click the CD-ROM icon on the desktop to access the contents. You can eject the CD-ROM at any time by right-clicking the CD-ROM icon and selecting the Eject device option, which will automatically unmount the CD-ROM.

If X does not automatically mount your CD-ROM (like when you are root) when inserted in the drive, you need to do the following:

- 1. Run the GNOME Control Center program by clicking the tool box icon on the Panel or by clicking the Main Menu button and choosing Programs → Settings → GNOME Control Center and then choosing Peripherals → CD Properties from the left-hand tree menu.
- 2. Select the Automatically Mount CD When Inserted option under the Data CDs section.

![](img/9eb7e89292d2f85707b4d49102c865b7_198_0.png)

> If you wish to mount a CD-ROM only when needed, you can disable the automatic mount option and simply right-click the CD-ROM icon on the desktop to mount it by choosing the Mount Device option.

- 3. Select the Run Command When CD is Inserted option under the Audio CDs section if you wish to play your audio CDs automatically. You can also specify an audio CD player command in the command-line entry box if you want, although the default `gtcd` player works quite well.

### Mounting a floppy disk

Mounting a floppy disk is quite simple. If you're running a remote shell or terminal window, insert the floppy disk and run the `mount /mnt/floppy`
