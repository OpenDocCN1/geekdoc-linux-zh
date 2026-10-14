
store the signature database securely before the install is complete. First, install the Tripwire package:

```
$ sudo apt-get install tripwire
```

If you don’t have an MTA (Mail Transport Agent) installed, the Tripwire package will add one as a dependency. As the Tripwire package installs, you will be asked a number of questions about keys. Tripwire uses two different keys to sign files and ensure that they have not been altered. The first key is a site-wide key that you might use for all of the servers on a particular network. The second key is a local key that is unique for this particular machine. If you do not yet have a site key or you aren’t sure what this means, answer Yes to create a site key. Next you get a similar prompt about a local key. Unless you already have a local Tripwire key, answer Yes here as well so the installer can create one. At the next prompt, answer Yes to rebuild the Tripwire configuration file, and Yes one final time to re-create the policy file. Finally, enter passphrases to use for the site and local keys. Be sure to note what passphrases you selected, because there’s no method to retrieve or reset them if you forget.

## Update Tripwire Policy

The Tripwire policy file is located at /etc/tripwire/twpol.txt and defines all of the files and directories Tripwire will monitor along with what information to monitor and how to respond to changes in each file. The default twpol.txt file is a good starting place, but it contains a few files and directories that you will want to remove to avoid a lot of false positives every time you run a Tripwire check. Open the file in a text editor and remove the lines as indicated for each file below:

- /etc/rc.boot
- Ubuntu doesn’t have this file, so remove the line that says

```
/etc/rc.boot   -> $(SEC_BIN) ;
```

- /proc
- Files in the /proc directory change constantly, so you will get tons of false alarms if this is scanned. Delete the following line from the file:

```
/proc   -> $(Device) ;
```

## /root

There is a large section of the twpol.txt file that lists files under the /root directory. The problem is that by default these files don't exist, so they will generate false positives. Locate the section of the file that looks like this:

```
# These files change the behavior of the root account
(
    rulename = "Root config files",
    severity = 100
)
{
    /root    -> $(SEC_CRIT) ; # Catch all additions to /root
```

Delete the references to all of the files under the /root directory except for /root/.bashrc. The resulting segment of the twpol.txt file looks like this:

```
# These files change the behavior of the root account
(
    rulename = "Root config files",
    severity = 100
)
{
    /root    -> $(SEC_CRIT) ; # Catch all additions to /root
    /root/.bashrc  -> $(SEC_CONFIG) ;
}
```

Save all of your changes, and then use the twadmin tool to update the policy file:

```
$ sudo twadmin -m P /etc/tripwire/twpol.txt
```

## Initialize the Tripwire Database

Once the policy file has been changed, you are ready to initialize the database. Note that the system's state at this point in time is what Tripwire considers the gold standard, so you want to initialize the database as soon as possible after the system has been created as possible. Here is the command to initialize Tripwire's database:

```
$ sudo tripwire -m i
```

Don’t worry about any errors you see about the /var/lib/tripwire/foo.twd file not existing—this is the database you are creating now. Once the database has been initialized, you should store it somewhere safe, because if attackers get root privileges they could update the database and hide their tracks. There are a few ways to secure the database. One, you could store the database on a floppy disk with the physical write-protect bit set and change the /etc/tripwire/twcfg.txt file to point to that new location. Alternatively, you could set up an NFS server that you consider secure to host all of the Tripwire database files and set all of the databases as read-only.

Since floppies are getting hard to come by, I describe how to set this up with NFS. Let’s assume that your Tripwire database is at /var/lib/tripwire/host1.twd. You have an NFS server at 10.1.1.7 and have copied the host1.twd file at /mnt/tripwire/host1/. Then you would use chmod 400 /mnt/tripwire/host1/host1.twd to ensure that the file could not be changed. Since Tripwire checks are run as the root user, you will probably have to disable root squashing on the NFS server, at least whenever you need to update the database. If you wanted additional security, you could also modify the /etc/exports file so that this share could be mounted only as read-only. NFS server administration is out of the scope of this chapter, but for more information on NFS server configuration, check the NFS section of Chapter 5. With NFS configured, create a directory called /mnt/tripwire on your local machine and mount the NFS share:

```bash
$ sudo mkdir /mnt/tripwire
$ sudo mount -o ro 10.1.1.7:/mnt/tripwire/host1/ /mnt/tripwire
```

If you get an error that this is an unknown file system type, be sure that you have the nfs-common package installed. Once the share mounts successfully, add a new line to /etc/fstab to make sure that it mounts automatically each time the system boots:

```text
10.1.1.7:/mnt/tripwire/host1 /mnt/tripwire nfs defaults,ro 0 0
```

Now if you run sudo ls -l /mnt/tripwire/, you should be able to see the /mnt/tripwire/host1.twd file (the filename will be named after your host’s
