> NOTE On Red Hat systems, you can also mount and unmount all your NFS file systems at once with the /etc/rc.d/init.d/netscript, which you can invoke with the service command. This script reads the NFS entries in the /etc/fstab file, using them to mount and unmount NFS remote directories. Using the stop argument unmounts the file systems, and with the start argument, you mount them again. The restart argument first unmounts and then remounts the file systems.

# Mounting NFS on Demand: autofs

You can also mount NFS file systems using the automount service, autofs. This requires added configuration on the client’s part. The autofs service will mount a file system only when you try to access it. A directory change operation (cd) to a specified directory will trigger the mount operation, mounting the remote file system at that time.

The autofs service is configured using a master file to list map files, which in turn lists the file systems to be mounted. The /etc/auto.master file is the autofs master file. The master file will list the root pathnames where file systems can be mounted along with a map file for each of those pathnames. The map file will then list a key (subdirectory), mount options, and the file systems that can be mounted in that root pathname directory. On some distributions, the /auto directory is already implemented as the root pathname for files systems automatically mounted. You could add your own in the /etc/auto.master file along with your own map files, if you wish. You will find that the /etc/auto.master file contains the following entry for the /auto directory, listing auto.misc as its map file:

```
/auto    auto.misc    --timeout 60
```

Following the map file, you can add options, as shown in the preceding example. The timeout option specifies the number of seconds of inactivity to wait before trying to automatically unmount.

In the map file, you list the key, the mount options, and the file system to be mounted. The key will be the subdirectory on the local system where the file system is mounted. For example, to mount the /home/projects directory on the rabbit.mytrek.com host to the /auto/projects directory, you would use the following entry:

```
projects  soft,intr,timeo=20  rabbit.mytrek.com:/home/projects
```

You could also create a new entry in the master file for an NFS file system, as shown here:

```
/myprojects    auto.myprojects    --timeout 60
```

You would then create an /etc/auto.myprojects file and place entries in it for NFS files system mounts, like the following:

```
dylan    soft,intr,rw    rabbit.mytrek.com:/home/projects
newgame  soft,intr,ro    lizard.mytrek.com:/home/supergame
```

> NOTE The autofs service can be used for any file systems, including floppy disks and CD-ROMs. See Chapter 30.