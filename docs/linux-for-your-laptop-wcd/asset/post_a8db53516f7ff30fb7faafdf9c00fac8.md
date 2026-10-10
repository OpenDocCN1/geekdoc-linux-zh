
used by NFS. On Red Hat, Mandrake, and Yellow Dog Linux systems, you can start the portmap daemon like this:

```
# /etc/rc.d/init.d/portmap start
Starting portmapper:                                          [  OK  ]
```

The script starts the software. You should see **OK** echoed back to your display. Next, ensure that NFS services have been started on your remote server. Use an `/etc/rc.d/init.d` script named *nfs*:

```
# /etc/rc.d/init.d/nfs start
Starting NFS services:                                       [  OK  ]
Starting NFS steid:                                          [  OK  ]
Starting NFS quotas:                                         [  OK  ]
Starting NFS mountd:                                         [  OK  ]
Starting NFS daemon:                                         [  OK  ]
```

As you can see, NFS services consist of several daemons that run in the background.

## Mounting the Filesystem

Your notebook should be hooked up to your network. As root, you can then use the `mount` command, along with its `-t` option, the remote server's name and directory (from `/etc/exports`), and a local mount point. For example, if your remote server is named *workhorse*, and you'd like to mount its `/d3/backup` directory to your notebook's `/mnt` directory, use the `mount` command like this:

```
# mount -t nfs -o rsize=8192,wsize=8192 workhorse:/d3/backup /mnt
```

The `-o` (option) entries are used to greatly speed up file transfers by specifying large read and write buffers. You can then verify that the remote directory has been mounted locally using the `ls` or `df` commands:

```
# df /mnt
Filesystem             Size  Used Avail Use% Mounted on
workhorse:/d3/backup   1.9G  770M  1.1G 41% /mnt
```

Assuming you have the correct access permission on the directory, you can then use the `cp` or `tar` commands to copy or create archives of your work into the backup directory:

```
# cp -a /home/bball/* /mnt
```

or

```
# tar cvzf /mnt/backup.tgz /home/bball
```

These commands will copy the entire contents of your home directory or create an archive of your home directory on the remote drive. When you've finished working with the remote directory, you can use the `umount` command to detach it from your local filesystem:

```
# umount /mnt
```

## Using the rsync Command

The `rsync` command, found under the /usr/bin directory, can be used to quickly transfer files between directories or partitions on your notebook or to a remote computer on your LAN or over the Internet. One of the great features of this command is that these transfers are much faster than normal backups because `rsync` recognizes when destination files match original files. The files are then skipped in the process of “synchronizing” the local and remote directories.

This command may be used to copy local files, to copy files from a local computer to a remote computer using a remote shell, or to copy files from a remote computer to a local computer. The `rsync` command also recognizes a special Uniform Resource Locator (URL), such as `rsync://`. This is useful for copying files from a remote server.

## Configuring rsync

The first step in configuring `rsync` is to log in as the root operator and then create identical /etc/rsyncd.conf files on your remote server and notebook. For example, on your server, perhaps named workhorse, you would create an rsyncd.conf entry that looks like this:

```
[bbell]
    comment = bbell file area
    path = /home/bbell
    read only = no
    list = yes
    hosts allow = zippo
```

The term in brackets ([ ]) is an identifying name for `rsync` known as a *module*. The `comment =` entry is for your use and is returned when you use `rsync` to list available services. The `path =` entry defines the source and destination of files to be transferred. The `read only =` entry is set to `no` so that files may be deleted or created. The `list = yes` entry enables the listing of the module and its information. The `hosts allow =` entry is used to list individual hostnames or IP addresses, or even a range of IP addresses and hostnames specified by wildcards. In this example, the notebook is named zippo.

The corresponding /etc/rsyncd.conf file on the notebook named zippo would look like this:

```
[ball]
    comment = ball file area
    path = /home/bball
    read only = no
    list = yes
    hosts allow = workhorse
```

You (as root) must then run `rsync` in its background (daemon) mode on your remote server and notebook, like this:

```
# rsync --daemon
```

You're now set to transfer files!

## Transferring Files

For example, if your notebook is connected to the LAN, and you'd like to synchronize a directory named `work` in your home directory on your notebook with an identical directory on your server named `workhorse`, you can use the `rsync` command, its `-v` options, and the local and remote directories like this:

```
# rsync -vva workhorse:/home/bball/work .
```

The `v` (verbose) option lists the files that are being transferred, and the `a` (archive) option copies files, symbolic links, subdirectories, and contents. The period (`.`) assumes that you are executing this command in your home directory on your notebook. This means that the preceding command could also look like this:

```
# rsync -vva workhorse:/home/bball/work /home/bball
```

## Synchronizing the Palm PDA

One of the most useful information appliances to hit the market in recent years (besides your notebook running Linux) is the Palm PDA (Personal Digital Assistant). These ubiquitous devices have captured the hearts and minds of millions of users, and many Linux users are especially fond of the lightweight, easy-to-use PDA. One of the reasons is that the Palm PDA is supported quite well by Linux. Today, nearly every Linux distribution includes software support that you can use to do the following:

- Back up the contents of your Palm to a specified directory
- Restore the contents of your PDA after a battery change
- Install specific software applications
- Delete one or more specified databases
- Retrieve a specific database
- List or display databases in the PDA
- Add records to databases
- And, most important, synchronize data between the contents of a specified directory and the contents of your Palm PDA

## Palm Computing “Gets It”

There are several reasons for the success of the Palm PDA in the marketplace (besides a great hardware design). One of these reasons is that 3Com, which debuted the Palm PDA, decided to open up the device’s software internals and publish nearly all the information needed by developers to write programs for the Palm. This information quickly led to free software tools (such as cross-compilers) for Linux that can be used to develop programs for the Palm for free. This is unlike Microsoft’s now-defunct WinCE, which has been dropped by a number of hardware manufacturers over the last year, and which cost developers hundreds of dollars just for software development tools. This year, 3Com has again re-entered the handheld market with yet another operating system (still based on WinCE 3.0) named PocketPC. Free and open information and software, or, costly, proprietary, and closed software? You be the judge.

Much of the magic that makes Linux and the Palm work well together is due to the efforts of Kenneth Albanowski and his pilot-link suite of commands. Table 12.1 lists the programs in this suite (although you can probably get by with just the *pilot-xfer* command).

Using this software is quite easy, but you’ll read about a few tricks in the next sections that can make file transfers even faster.

## Table 12.1 Main Pilot-Link Software

| **Command** | **Description** |
| :--- | :--- |
| addresses | Retrieves the address book to a text file |
| debugsh | Accesses the Palm debug monitor |
| dlpsh | Controls the Palm HotSync commands |
| getrom | Retrieves the Palm ROM |
| install-datebook | Installs a text file as a datebook |
| install-memo | Installs a text file as a Palm memo |
| install-todos | Installs a text file as a Palm To-do |
| install-user | Changes PDA user settings |
| memos | Retrieves memos from the PDA |
| pilot-addresses | Retrieves and installs the address book |
| pilot-clip | Retrieves and installs clipboard data |
| pilot-debug | Runs the Palm debug monitor |
| pilot-dedupe | Deletes duplicate Palm records |
| pilot-file | Displays information about Palm files |
| pilot-mail | Installs mail into the Palm mail application |
| pilot-schlep | Installs a file on the Palm |
| pilot-undelete | Undeletes Palm records |
| pilot-xfer | A do-all command for the Palm |
| read-expenses | Retrieves expense database info from Palm |
| read-ical | Retrieves and saves the Palm datebook to ical format |
| read-todos | Retrieves the To-Do database to text |
| reminders | Retrieves, converts the Palm datebook to a remind data file format |
| sync-plan | Synchronizes the Palm datebook with the plan calendar client |
