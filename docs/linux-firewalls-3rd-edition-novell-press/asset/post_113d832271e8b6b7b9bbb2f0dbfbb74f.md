
## Scheduling AIDE to Run Automatically

AIDE is best run using a cron job (scheduled task). Therefore, you should schedule AIDE to run automatically without your intervention. AIDE is commonly run once per day, but you should schedule it to run according to your security policy. The easiest and quickest method to have AIDE run daily is to create a crontab entry.

Creating a crontab entry is a matter of running this (as root):

```
crontab -e
```

To run AIDE nightly at 2:00 a.m., enter the following line into crontab:

```
0 2 * * * /usr/local/bin/aide --check
```

For more information on the format of crontab entries, see your distribution's documentation.

## Monitoring AIDE for Bad Things

Okay, so you have this shiny new filesystem integrity-checking tool all set up and running. But now what? Now you sit and wait for something to happen. Usually nothing does, and even when it appears that something bad might have happened, many times it hasn't.

AIDE will continue to monitor the filesystem according to the rules you configured. Thanks to the cron job, you'll receive reports nightly containing the files and the attributes for those files that have changed since the database was initialized or last updated. Many times these changes will be completely benign. Recall the example from the beginning of the chapter. If you add a user, files such as `/etc/passwd` and `/etc/shadow` will change. AIDE will notice and report accordingly, assuming that you're checking `/etc`. However, if you didn't add a user or make other changes to `/etc/passwd` or `/etc/shadow`, it might bear closer examination to make sure that an attacker hasn't altered either one of those important files.

Of course, there are other files that AIDE will be reporting on. You should closely monitor the AIDE report for files that were altered unexpectedly. For example, the files `/bin/su` or `/usr/bin/passwd` should rarely be altered and then only by certain known software updates. Therefore, if a file such as `/bin/su` shows up in an AIDE report, you need to look into it immediately to see when and why that file changed. Taking this example one step further, assume for a moment that AIDE ran overnight through its normal process. In the morning you awake to find an email containing some of the following lines:

```
AIDE found differences between database and filesystem!!
Start timestamp: 2004-03-09 20:24:33
Summary:
Total number of files=1488, added files=0, removed files=0, changed files=1

Changed files:
changed:/bin/su
Detailed information about changes:

File: /bin/su
Size: 23176, 0
Permissions: -rwSr-xr-x, -rwxr-xr-x
Mtime: 2002-04-07 10:59:14, 2004-03-09 20:24:31
Ctime: 2002-04-08 20:45:36, 2004-03-09 20:24:31
Inode: 98564, 100922
MD5: XTJX0HkkY/492djseGo8x7A==, 1B2M2Y8AsgTpgAmYTPhCfCg==
```

The AIDE check that you scheduled found something. You can quickly tell from the summary line what has been found:

```
Summary:
Total number of files=1488, added files=0, removed files=0, changed files=1
```

Next you'll see a slightly more detailed summary of the files that have been added, changed, or removed since the database was initialized or last updated. In this case, there's only one file that's been changed, /bin/su:

```
Changed files:
changed:/bin/su
```

Finally, you see the gory details of exactly what AIDE found for the files in the report. The items you see in the detail section of the report correspond to the type of check that you configured in aide.conf; if you do remember that, right? In this case, six items changed, the file size, permissions, Mtime (modified time), Ctime (creation time), inode, and MD5 hash:

```
File: /bin/su
Size: 23176, 23948
Permissions: -rwSr-xr-x, -rwxr-xr-x
Mtime: 2002-04-07 10:59:14, 2004-03-09 20:24:31
Ctime: 2002-04-08 20:45:36, 2004-03-09 20:24:31
Inode: 98564, 100922
MD5: XTJX0HkkY/492djseGo8x7A==, 1B2M2Y8AsgTpgAmYTPhCfCg==
```

Based on this report, it's easy to see that something changed with /bin/su and probably not for the better. Knowing that I didn't perform any updates to the server in the past few days, I can reasonably assume that a break-in has occurred and someone has replaced the normal su program with one of his own. An attacker might do this so that he can steal the root password or, more likely, he would do it so that he always has a way to get root access into the server. The attackers trojaned su program might always allow users to get to root if they type a certain password (not the real root password) or if they log in as a certain user. In this manner, no matter what I change the root password to, the attacker can always get root access.

Without a utility such as AIDE I might not see that /bin/su has changed. It's still roughly the same size and the permissions are the same. A more skilled attacker would've also changed the Ctime to match an earlier time, to make it appear that the file is older than it really is. In that way, an ls -la on the file wouldn't have given many clues as to the real status of this important program.

The /bin/su example is just one of many in a long line of similar examples. Attackers can and will replace your programs with their own versions to hide their activity or give them elevated privileges. For example, a common attack practice is to place a trojaned ps program on a server to hide the attacker's processes. Performing a ps aux to look at what processes are running wouldn't reveal the attacker's processes if the trojaned version is in place. Another attacker might replace the cron scheduling program with one of his own that automatically runs his attack again after you've cleaned up from it the first time!

### Cleaning Up the AIDE Database

Over time, you'll notice that AIDE check reports become longer and longer. This is usually the result of normal activity on the server, such as adding and deleting users, updating software, and changing settings in configuration files. You should regularly update the AIDE database not only to shorten reports but also to better track when unexpected changes occur. If you don't regularly update the AIDE database, you might miss a change that resulted from an attack.

You may be asking, "How often should I update the AIDE database?" The answer depends largely on your needs and your security policy. When you first start to use AIDE, I expect that you should be updating the database at least for the first few runs (again, depending on your security policy) and, more important, refining the configuration file. You'll find that certain files change so often that you need to either exclude them entirely or change the types of checks that occur on those files.

It is much better to change the types of checks than to simply skip the files altogether. Some file attributes that AIDE can check will not change often or at all for the same file. Attributes such as inode and Ctime shouldn't change. Therefore, if you notice certain files that keep showing up in the AIDE report and you've ruled out nefarious activity, you should change the type of check that occurs on that file within the AIDE configuration file.

A file that regularly changes on some systems is the Samba password file, /etc/samba/smbpasswd. On such systems, the file regularly shows up in the report where everything in the /etc/ directory is examined using the R check (refer to Table 12.1 for a refresher). A more appropriate check type for this file might include things that don't change often such as inode and Ctime. Such a check would appear like this in the AIDE configuration file:

```
/etc/samba/smbpasswd c+i
```

## Changing the Output of the AIDE Report

Note the use of the $ at the end of the filename in the example to indicate the end of line.

As the AIDE report runs, you'll be able to use more granularity to refine the files that are checked and the checks themselves. After you update the AIDE configuration file, you'll need to update the database so that the changes take effect. This process is accomplished by running this command:

```
/usr/local/bin/aide --update
```

After the update is complete, you'll have a new database file, /usr/local/etc/aide.db.new by default. This file should be moved to overwrite the existing database:

```
mv /usr/local/etc/aide.db.new /usr/local/etc/aide.db
```

Now running aide --check will give a clean result:

```
AIDE, version 0.10

All files match AIDE database. Looks okay!
```

After you update the database, you should copy the file to secure media or to another computer to ensure the integrity of the database.

With the AIDE configuration file and database updated and AIDE scheduled to run nightly, you now have an infrastructure in place to verify the integrity of your filesystem. From here, you can read on to find out about more advanced configurations for AIDE, or you can jump ahead to the next part of the chapter to find out about the rootkit checking tool called Chkrootkit.

## Changing the Output of the AIDE Report

You might want a little more flexibility in the location of the AIDE report. For example, you may not want to receive emails if everything is okay with the AIDE report, or you may want to have AIDE report into a file instead of providing standard output. AIDE has four basic options for configuring output that can be configured through the AIDE configuration file.

> **LINUX OUTPUT STREAMS**
>
> Linux has three generic streams of output that are created when a program runs. These streams are referred to as STDIN, STDOUT, and STDERR, which are abbreviations for Standard Input, Standard Output, and Standard Error, respectively. When you see a referral to STDOUT, it refers to the normal method of output to the screen, and STDERR indicates output as a result of an error condition. As you might expect, STDIN refers to the method of input when read from the input file descriptor.
