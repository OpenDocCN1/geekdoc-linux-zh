
log of the backup can also be created during the backup by redirecting the standard output like this:

```
# cp -avR directory_to_backup destination_vol_or_dir 1>/root/backup_log.txt
```

or

```
# cp -avR fedora /test2 1>/root/backup_log.txt
```

This example makes an exact copy of the directory named /fedora on the volume named /test2, and saves a backup report named backup_log.txt under /root.

## Copying Files Using cpio

You can use cpio instead of tar to make backup file copies, but remember that cpio really works with lists of files. So you must first create the list and feed it to cpio.

```
# find source_directory -print | cpio -pudv target_directory
```

Here, use the find command on the current directory with the -print option to generate a list of files in that directory. Then pipe that file list to cpio. When cpio gets the file list, it

- -p—Runs in copy-pass mode. (We are not creating an archive file here.)
- -u—Replaces all files without asking (unconditional).
- -d—Creates directories if needed.
- -v—Lists all files copied (verbose).

## Copying Files Using mc

The Midnight Commander is a command-line file manager that is useful for copying, moving, and archiving files and directories. The Midnight Commander has a look and feel similar to the Norton Commander of DOS fame. By executing mc at a shell prompt, a dual-pane view of the files is displayed. It contains drop-down menu choices and function keys to manipulate files. It also uses its own virtual file system, enabling it to mount FTP directories and display the contents of tar files, gzipped tar files (.tar.gz or .t2), bzip files, DEB files, and RPM files, as well as extract individual files from them. As if that was not enough, mc contains a File Undelete virtual file system for ext2/3 partitions. By using cd to “change directories” to an FTP server’s URL, you can transfer files using the FTP protocol. The default font chosen for Fedora Core makes the display of mc ugly when used in a tty console (as opposed to an xterm), but does not affect its performance.

Figure 16.4 shows a shot of the default dual-panel display. Pressing the F9 key drops down the menu, and pressing F1 displays the Help file. A “feature” in the default GNOME terminal intercepts the F10 key used to exit mc, so use F9 instead to access the menu item to quit, or simply click on the menu bar at the bottom with your mouse. The configuration files are well documented, and it would appear easy to extend the functionality of mc for your system if you understand shell scripting and regular expressions. It is an excellent choice for file management on servers not running X.

![](img/774d40fd20903495c5cd00e2efad3f33_472_0.png)

FIGURE 16.4 The Midnight Commander is a highly versatile file tool. If it does not display properly on your screen, launch it with the -a argument to force ASCII mode.

## Copying Files Using scp

The traditional way to copy files from one computer to another is to use uucp, the Unix-to-Unix copy program, or to use one of the rtools, rcp. The rtools are insecure over a public network and are subject to several exploits. It is best not to use them at all because they have been supplanted by more secure tools based on the secure shell, ssh.

> NOTE
> The file transfer protocol known as FTP can be used to copy files from one computer to another, but this requires that an FTP server be running, and the server is subject to security problems of its own.
> See Chapter 22, “Remote File Serving with FTP,” for more details on FTP.

The scp command uses ssh for file copying. Useful arguments for this command include

- -p—Preserves modification times, access times, and modes from the original file.
- -r—Recursively copies entire directories.
- -v—Verbose mode for debugging problems.
- -C—Enables file compression.

The syntax of an scp copy command is

```
scp [arguments] [source] [target]
```

For example, if we want to copy the file /home/paul/fedora.txt to ~/docs on our account on a remote host

```
$ scp -p /home/paul/fedora.txt paul@192.168.168.4:/home/paul/docs
```

After it prompts us for a password, we see

```
fedora.txt      100%  *****************************   0  00:00
```

This indicates that the transfer was completed. If we had subdirectories to transfer, we would have used the -r (recursive) argument.

Actually, it can be much easier than the example because scp assumes that all paths are relative to the home directory of the user unless the full path is given.

Taking this into consideration, our example becomes

```
$ scp -p fedora.txt paul@192.168.5:docs
```

And it can be made even easier. Creating a file named ~/.ssh/config with the following contents:

```
Host = titan
HostName = 192.168.168.5
User = paul
ForwardAgent = yes
ForwardX11 = yes
Compression = yes
```

allows us to simply use

```
$ scp -p fedora.txt titan:docs
```

> **NOTE**
>
> If you are comfortable with FTP, you might want to consider a cousin of scp: sftp. It provides the common FTP command set. If no sftp server is running on the remote host, simply use scp to copy the sftpserver binary to your remote home directory. (Often, /bin is in your path.) The FTP client gftp supports sftp and gives you a GUI client as well.
>
> You can find more information on both scp and sftp in Chapter 25, "Remote Access with SSH and Telnet."

## Copying Files Using rsync

rsync is a file transfer tool now included with Fedora Core. According to the rsync man page, it is a “faster, flexible replacement for rcp, the traditional remote copy application.” We have already mentioned that rcp is not a secure method of transferring files.

A significant benefit of using rsync is that it speeds up file transfers by transferring only the differences between the two sites across a network link. rsync can copy links, devices, owners, groups, and permissions, and it can be told to exclude certain files. rsync can use ssh (via the command line or setting the RSYNC_RSH variable) and does not require root privileges. rsync has support for anonymous or authenticated rsync servers for use in mirroring.

The man page is extremely well-written and provides four excellent examples of how rsync can be used to transfer files matching a pattern, can recursively transfer files, and can be used locally (without a server).

The rsync command has some 62 options (not including short and long variants of the same option). A few particularly useful options are

- **-z**—Uses gzip compression.
- **-P**—Keeps partial files and reports on the progress of the transfer.
- **--bwlimit=KBPS**—Sets a maximum bandwidth rsync might use.
- **--exclude-from=FILE**—All excluded files listed in a separate file; pattern matching is enabled.
- **-x**—Does not cross file system boundaries.
- **-n**—Dry run for testing.
- **-l**—Copies symlinks, not the files themselves.
- **-L**—Copies the file, not the symlink.
- **-r**—Copies recursively.
- **-v**—Verbose output.

The rsync utility can be run as a daemon to establish an rsync server, listening on TCP port 873 by default. The configuration of the server is handled by the contents of the /etc/rsyncd.conf file; the man page for rsyncd.conf provides the details. The daemon can be launched standalone or via xinetd to suit your needs.

The rsync website provides an examples page showing examples of

- Backing up to a central server with a seven-day increment
- Backing up to a spare disk
- Mirroring a CVS tree
- Automated backup at home over a modem

A time and bandwidth saving trick is to use `rsync` to only re-download that part of an ISO file that is incorrect, rather than downloading the entire 650MB-700MB of the file. First, you must locate an `rsync` server that is offering the .iso images you seek. Look at the Fedora Core mirrors at http://www.redhat.com/download/mirror.html and select one that offers "D", the identifier for .iso images.

An `rsync` server will provide *modules*, or directory trees as symbolic names. To determine if a server provides an `rsync` module, use the query:

```
rsync some.site.com::
```

If an `rsync` server is running on that site, you will see a list of available `rsync` modules. If we try

```
$ rsync ftp-linux.cc.gatech.edu::
```

```
GEORGIA TECH SOFTWARE LIBRARY

Unauthorized use is prohibited. Your access is being logged.

If you run a publicly accessible mirror, and are interested in
mirroring from us, please contact lxmirror@cc.gatech.edu.
```

altlinux    mirror of ftp.altlinux.ru
arklinux    mirror of arklinux.org
asplinux    mirror of ftp.asp-linux.com
debian      mirror of ftp.debian.org
debian-cd   mirror of ftp.debian.org
mandrake    mirror of ftp.mandrake.com
redhat      mirror of ftp.redhat.com
<SNIP>

To use this `rsync` service, we would explore the *redhat* module to discover the file path to the .iso images using `rsync -r` and the module name to explore it recursively.

To use `rsync` to repair our defective .iso images, we point `rsync` at the "good" image and at our "bad" image like so:

```
# rsync -a -vvv --progress ftp-linux.cc.gatech.edu:\\ 
redhat/linux/9/en/iso/i386/shrike-i386-disc1.iso\\ 
~/downloads/shrike-i386-disc1.iso
```

`rsync` compares the two files and will download only the needed replacement parts for our local file much faster than downloading the entire image again.
