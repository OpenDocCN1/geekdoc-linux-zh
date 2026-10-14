
```
me@linuxbox ~$ touch playground/dir-099/file-Z
me@linuxbox ~$ rsync -av playground foo
building file list ... done
playground/dir-099/file-Z
sent 22685 bytes  received 43 bytes  45454.00 bytes/sec
total size is 3230  speedup is 0.14
```

As a practical example, let’s consider the imaginary external hard drive that we used earlier with tar. If we attach the drive to our system and, once again, it is mounted at /media/BigDisk, we can perform a useful system backup by first creating a directory named /backup on the external drive and then using rsync to copy the most important stuff from our system to the external drive:

```
me@linuxbox ~$ mkdir /media/BigDisk/backup
me@linuxbox ~$ sudo rsync -av --delete /etc /home /usr/local /media/BigDisk/backup
```

In this example, we copied the /etc, /home, and /usr/local directories from our system to our imaginary storage device. We included the --delete option to remove files that may have existed on the backup device that no longer existed on the source device (this is irrelevant the first time we make a backup but will be useful on subsequent copies). Repeating the procedure of attaching the external drive and running this rsync command would be a useful (though not ideal) way of keeping a small system backed up. Of course, an alias would be helpful here, too. We could create an alias and add it to our .bashrc file to provide this feature:

```
alias backup='sudo rsync -av --delete /etc /home /usr/local /media/BigDisk/backup'
```

Now all we have to do is attach our external drive and run the backup command to do the job.

## Using rsync over a Network

One of the real beauties of rsync is that it can be used to copy files over a network. After all, the r in rsync stands for remote. Remote copying can be done in one of two ways.

The first way is with another system that has rsync installed, along with a remote shell program such as ssh. Let’s say we had another system on our local network with a lot of available hard drive space and we wanted to perform our backup operation using the remote system instead of an external drive. Assuming that it already had a directory named /backup where we could deliver our files, we could do this:

```
[me@linuxbox ~]$ sudo rsync -av --delete --rsh=ssh /etc /home /usr/local remote-sys:/backup
```

We made two changes to our command to facilitate the network copy. First, we added the --rsh=ssh option, which instructs rsync to use the ssh program as its remote shell. In this way, we were able to use an SSH-encrypted tunnel to securely transfer the data from the local system to the remote host. Second, we specified the remote host by prefixing its name (in this case the remote host is named remote.sys) to the destination pathname.

The second way that rsync can be used to synchronize files over a network is by using an rsync server. rsync can be configured to run as a daemon and listen to incoming requests for synchronization. This is often done to allow mirroring of a remote system. For example, Red Hat Software maintains a large repository of software packages under development for its Fedora distribution. It is useful for software testers to mirror this collection during the testing phase of the distribution release cycle. Since files in the repository change frequently (often more than once a day), it is desirable to maintain a local mirror by periodic synchronization, rather than by bulk copying of the repository. One of these repositories is kept at Georgia Tech; we could mirror it using our local copy of rsync and Georgia Tech’s rsync server like this:

```
[me@linuxbox ~]$ mkdir fedora-devel
[me@linuxbox ~]$ rsync -av --delete rsync://rsync.gtlib.gatech.edu/fedora-linux-core/development/i386/os fedora-devel
```

In this example, we use the URI of the remote rsync server, which consists of a protocol (rsync://), followed by the remote hostname (rsync.gtlib.gatech.edu), followed by the pathname of the repository.

## 19

## REGULAR EXPRESSIONS

In the next few chapters, we are going to look at tools used to manipulate text. As we have seen, text data plays an important role on all Unix-like systems, such as Linux. But before we can fully appreciate all of the features offered by these tools, we have to examine a technology that is frequently associated with the most sophisticated uses of these tools—regular expressions.

As we have navigated the many features and facilities offered by the command line, we have encountered some truly arcane shell features and commands, such as shell expansion and quoting, keyboard shortcuts, and command history, not to mention the vi editor. Regular expressions continue this "tradition" and may be (arguably) the most arcane feature of them all. This is not to suggest that the time it takes to learn about them is not worth the effort. Quite the contrary. A good understanding will enable us to perform amazing feats, though their full value may not be immediately apparent.
