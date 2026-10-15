
When given a filename as its argument, the script will try to restore that file or directory (if there’s only one match), or it will show a list of candidates for restoration and allow the user to specify which version of the deleted file or directory to restore.

## The Results

Without any arguments specified, the script shows what’s in the deleted files archive as Listing 2-8 shows.

```
$ unrm
Contents of your deleted files archive (sorted by date):
detritus          this is a test
detritus           garbage
```

> Listing 2-8: Running the unrm shell script with no arguments lists the current files available to restore

When a filename is specified, the script displays more information about the file if there are multiple files with that name, as shown in Listing 2-9.

```
$ unrm detritus
More than one file or directory match in the archive:
1) detritus (size = 7688Kb, deleted = 11/29 at 10:00:12)
2) detritus (size = 4Kb, deleted = 11/29 at 09:59:51)
Which version of detritus should I restore ('0' to quit)? [1] : 0
unrm: Restore canceled by user.
```

> Listing 2-9: Running the unrm shell script with a single argument attempts to restore the file

## Hacking the Script

If you use this script, be aware that without any controls or limits, the files and directories in the deleted files archive will grow without bound. To avoid this, invoke find from within a cron job to prune the deleted files archive, using the -mtime flag to identify those files that have been sitting untouched for weeks. A 14-day archive is probably quite sufficient for most users and will keep the archival script from consuming too much disk space.

While we’re at it, there are some improvements that could make this script more user friendly. Think about adding starting flags like -1 to restore latest and -0 to delete 0 additional copies of the file. Which flags would you add, and how would they streamline processing?

## #17 Logging File Removals

Instead of archiving deleted files, you may just want to keep track of what deletions are happening on your system. In Listing 2-10, file deletions with the rm command will be logged in a separate file without notifying the user. This can be accomplished by using the script as a wrapper. The basic idea of wrappers is that they live between an actual Unix command and the user, offering the user useful functionality that's not available with the original command alone.

> Wrappers are such a powerful concept that you'll see them show up time and again as you go through this book.

### The Code

```
#!/bin/bash
# logrm--logs all file deletion requests unless the -s flag is used

removelog="/var/log/remove.log"

① if [ "$#" -eq 0 ] ; then
    echo "Usage: $0 [-s] list of files or directories" >&2
    exit 1
fi

② if [ "$1" = "-s" ] ; then
    # Silent operation requested ... don't log.
    shift
else
③   echo "$(date): $(USER): $0 $@" >> $removelog
fi

④ /bin/rm "$@"

exit 0
```

> Listing 2-10: The logrm shell script

### How It Works

The first section ① tests the user input, generating a simple file listing if no arguments are given. Then at ②, the script tests whether argument 1 is -s; if so, it skips logging the removal request. Finally, the timestamp, user, and command are added to the $removelog file ③ and the user command is silently passed over to the real /bin/rm program ④.

### Running the Script

Rather than giving this script a name like logrm, a typical way to install a wrapper program is to rename the underlying command it's intending to wrap and then install the wrapper using the original command's old name. If you choose this route, however, make sure that the wrapper invokes the newly renamed program, not itself! For example, if you rename /bin/rm to /bin/rm.old, and name this script /bin/rm, then the last few lines of the script will need to be changed so that it invokes /bin/rm.old instead of itself.

Alternatively, you can use an alias to replace standard rm calls with this command:

```
alias rm=logrm
```

In either case, you will need write and execute access to /var/log, which might not be the default configuration on your particular system.

### The Results

Let’s create a few files, delete them, and then examine the remove log, as shown in Listing 2-11.

```
$ touch unused.file ciao.c /tmp/junkit
$ logrm unused.file /tmp/junkit
$ logrm ciao.c
$ cat /var/log/remove.log
Thu Apr 6 11:32:05 MDT 2017: susan: /tmp/central.log
Fri Apr 7 14:25:11 MDT 2017: taylor: unused.file /tmp/junkit
Fri Apr 7 14:25:14 MDT 2017: taylor: ciao.c
```

> Listing 2-11: Testing the logrm shell script

Aha! Notice that on Thursday, user Susan deleted the file /tmp/central.log.

### Hacking the Script

There’s a potential log file ownership permission problem here. Either the remove.log file is writable by all, in which case a user could clear its contents out with a command like cat /dev/null > /var/log/remove.log, or it isn’t writable by all, in which case the script can’t log the events. You could use a setuid permission—with the script running as root—so that the script runs with the same permissions as the log file. However, there are two problems with this approach. First, it’s a really bad idea! Never run shell scripts under setuid! By using setuid to run a command as a specific user, no matter who is executing the command, you are potentially introducing security weaknesses to your system. Second, you could get into a situation where the users have permission to delete their files but the script doesn’t, and because the effective uid set with setuid would be inherited by the rm command itself, things would break. Great confusion would ensue when users couldn’t even remove their own files!

If you have an ext2, ext3, or ext4 filesystem (as is usually the case with Linux), a different solution is to use the chattr command to set a specific append-only file permission on the log file and then leave it writable to all without any danger. Yet another solution is to write the log messages to syslog, using the helpful logger command. Logging the rm commands with logger is straightforward, as shown here:

```
logger -t logrm "$(USER:-LOGNAME): $*"
```
