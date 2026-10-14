
we see that rsync detected the change and copied only the updated file.

As a practical example, let’s consider the imaginary external hard drive that we used earlier with tar. If we attach the drive to our system and, once again, it is mounted at /media/BigDisk, we can perform a useful system backup by first creating a directory named /backup on the external drive, and then using rsync to copy the most important stuff from our system to the external drive:

```
[me@linuxbox ~]$ mkdir /media/BigDisk/backup
[me@linuxbox ~]$ sudo rsync -av --delete /etc /home /usr/local /media/BigDisk/backup
```

In this example, we copied the /etc, /home, and /usr/local directories from our system to our imaginary storage device. We included the --delete option to remove files that may have existed on the backup device that no longer existed on the source device (this is irrelevant the first time we make a backup, but will be useful on subsequent copies). Repeating the procedure of attaching the external drive and running this rsync command would be a useful (though not ideal) way of keeping a small system backed up. Of course, an alias would be helpful here, too. We could create an alias and add it to our .bashrc file to provide this feature:

```
alias backup='sudo rsync -av --delete /etc /home /usr/local /media/BigDisk/backup'
```

Now all we have to do is attach our external drive and run the backup command to do the job.

## Using rsync Over A Network

One of the real beauties of rsync is that it can be used to copy files over a network. After all, the “r” in rsync stands for “remote.” Remote copying can be done in one of two ways. The first way is with another system that has rsync installed, along with a remote shell program such as ssh. Let’s say we had another system on our local network with a lot of available hard drive space and we wanted to perform our backup operation using the remote system instead of an external drive. Assuming that it already had a directory named /backup where we could deliver our files, we could do this:

```
[me@linuxbox ~]$ sudo rsync -av --delete --rsh=ssh /etc /home /usr/local remote-sys:/backup
```

We made two changes to our command to facilitate the network copy. First, we added the --rsh=ssh option, which instructs rsync to use the ssh program as its remote shell. In this way, we were able to use an ssh encrypted tunnel to securely transfer the data from the local system to the remote host. Second, we specified the remote host by prefixing its name (in this case the remote host is named remote-sys) to the destination pathname.

The second way that rsync can be used to synchronize files over a network is by using an rsync server. rsync can be configured to run as a daemon and listen to incoming requests for synchronization. This is often done to allow mirroring of a remote system. For example, Red Hat Software maintains a large repository of software packages under development for its Fedora distribution. It is useful for software testers to mirror this collection during the testing phase of the distribution release cycle. Since files in the repository change frequently (often more than once a day), it is desirable to maintain a local mirror by periodic synchronization, rather than by bulk copying of the repository. One of these repositories is kept at Georgia Tech; we could mirror it using our local copy of rsync and their rsync server like this:

```
[me@linuxbox ~]$ mkdir fedora-devel
[me@linuxbox ~]$ rsync -av --delete rsync://rsync.gtlib.gatech.edu/fedora-linux-core/development/i386/os fedora-devel
```

In this example, we use the URI of the remote rsync server, which consists of a protocol (rsync://), followed by the remote host-name (rsync.gtlib.gatech.edu), followed by the pathname of the repository.

## Summing Up

We've looked at the common compression and archiving programs used on Linux and other Unix-like operating systems. For archiving files, the tar/gzip combination is the preferred method on Unix-like systems while zip/unzip is used for interoperability with Windows systems. Finally, we looked at the rsync program (a personal favorite) which is very handy for efficient synchronization of files and directories across systems.

## Further Reading

- The man pages for all of the commands discussed here are pretty clear and contain useful examples. In addition, the GNU Project has a good online manual for its version of tar. It can be found here:
