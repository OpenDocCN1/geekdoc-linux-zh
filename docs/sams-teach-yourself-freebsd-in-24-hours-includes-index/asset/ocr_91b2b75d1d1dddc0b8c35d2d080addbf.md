# The /etc/make.conf File

The /etc/make.conf file contains settings that the C compiler will use when rebuilding the system from the source code you just downloaded. Another file, called /etc/defaults/make.conf, contains the default options that the C compiler will use. However, you do not want to make any changes to the /etc/defaults/make.conf file. Instead, make the changes to /etc/make.conf (creating it yourself if it does not already exist, as is the case in the default installation). This file will override the defaults given in /etc/defaults/make.conf. For most people, adding the following two lines to /etc/make.conf should suffice:

```
CFLAGS= -O pipe
NOPROFILE= TRUE
```

Note that the option after CFLAGS is a capital letter O and not a zero. This option tells the C compiler to apply certain optimizations when it compiles the code. The second line tells the compiler not to build profiled binaries. Profiled binaries are useful for debugging, but they also increase the size of the binary and reduce performance. So most users will probably want the NOPROFILE option set to TRUE.

After you have made these changes, save and exit the /etc/make.conf file.

# Updating Important Files

In some cases, certain configuration files might need to be updated before the system upgrade is actually performed because certain new versions of FreeBSD might expect, for example, certain user accounts or groups to exist for system purposes. If these groups and accounts did not exist in earlier versions of FreeBSD, the update process can fail.

The easiest way to upgrade these files is to use the program called mergemaster.sh. Start it with the -p option so that it only updates files that are important to the pre-upgrade. You don't want to update the rest of the files yet. For example,

```
mergemaster.sh -p
```

![](bbox=[0.15, 0.82, 0.25, 0.9])

> It's very important to back up your /etc directory before running mergemaster. Simply copy it to a new location, for example by entering cp -R /etc /etc.old. This way, if you accidentally overwrite a file in /etc, you can retrieve the old one with a minimum of pain.