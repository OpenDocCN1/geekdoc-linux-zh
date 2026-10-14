ing.). In addition, you need to disable root squashing and set the share to rw during the short time the database is updated. You will also need to remount the NFS share as rw. Once the NFS server is ready, go to the host itself and locate the report that contains the errors you want to override. This will probably be the newest file in /var/lib/tripwire/report. Then run the following Tripwire command to update the database:

```
$ sudo tripwire -m u -r /var/lib/tripwire/report/
hostname-20090107-190736.twr
```

Replace the filename under here with the name of your report. The update tool outputs the report to the screen in the root user's default text editor (probably vi, unless you set the EDITOR environment variable to something else). If this is the default vi editor, you should be able to use the arrow keys (or the standard H, J, K, and L keys) to move throughout the report. Each item slated to be updated in the database will be on a line with [x] at the beginning. As long as that x is inside the box, that file will be updated. If you do not want to update a particular file, move the cursor over that x and type r and then the spacebar to remove it. When you are finished editing the file, hit :wq. You will be prompted for the local key, and then the database will be updated.

Once this command is finished and the database is updated, you must go back to the NFS server and reinstate all of the permissions and other protections you put in place to make this file read-only.

# Ubuntu Tripwire Conventions

+   - **/etc/tripwire/**
+     This directory contains all of the main configuration files used by Tripwire.

+   - **/etc/tripwire/*-local.key and /etc/tripwire/site.key**
+     These files are your local and site keys, respectively. The local key will be named after the localhost.

+   - **/etc/tripwire/tw.cfg and /etc/tripwire/twcfg.txt**
+     The tw.cfg is the encrypted database of Tripwire settings, and the twcfg.txt is the plain-text version. Whenever you want to change