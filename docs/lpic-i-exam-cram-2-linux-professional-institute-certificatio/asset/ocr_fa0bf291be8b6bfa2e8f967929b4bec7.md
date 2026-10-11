The update commands must be run as root, and either one will do the job:
```text
updatedb
slocate -u
```

Sometimes you'll want to exclude files or directories from the *locate* database because they either are inappropriate or simply take too long to index without any apparent benefit. This is configurable in the `/etc/updatedb.conf` file. This file is read and the variables are used by the updating commands.

The two main methods of excluding objects in the configuration file are either by file system type or path. The following output is an example of a working `/etc/updatedb.conf` file:

```
```
PRUNEFS="devpts NFS nfs afs sfs proc smbfs autofs auto iso9660*"
PRUNEPATHS="*/tmp /usr/tmp /var/tmp /afs /net /sfs"
export PRUNEFS
export PRUNEPATHS
```
```

The *PRUNEFS* keyword is for file system types you want excluded from the *locate* database update; as you might expect, the *PRUNEPATHS* keyword is for directory trees you want excluded. Notice that most of the paths are temporary data locations or automount and exotic file locations.

![](bbox=[0.08, 0.49, 0.21, 0.58])

Remember for the exam that *locate* returns results for the search string in any portion of the path or filename it finds the string in. There will be questions that *locate* is right for, and some that really want the *whereis* command.

# # Finding Files

The *find* command is the most accurate but time-consuming method for searching the system for file objects. The command consists of several (sometimes confusing) sections. But, if it's learned properly, it can be a powerhouse for the busy sysadmin.

The structure of a *find* command is
*find startpath options arguments*

To make sense of this jumble of sections, let's take a look at a useful *find* command and match up the sections:
```text
find /home -iname *.mp3
/home/snuffy/g3 - red house.mp3
```

The previous command sets the start path to the `/home` directory and then looks for any instance of the string *mp3* as a file extension, or after the last . in the filename. It found a file in the user *snuffy*'s home directory and returned the full path for that file.