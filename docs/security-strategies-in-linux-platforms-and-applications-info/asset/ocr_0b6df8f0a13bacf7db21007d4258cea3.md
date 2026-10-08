# PART 3 Building a Layered Linux Security Strategy

A simple method to monitor a system for source code is to look for tarballs, which are normally provided in one or two compressed file archives, normally with .tar.gz or .tar.bz2 extensions. They can be found in user home directories with the find command. Specifically, the following command starts with the /home/ directory and searches all subdirectories for files with the .tar.gz extension:

```
# find/home/ -name *.tar.gz
```

As desired, commands can run on a regular basis as a cron job. For example, to set up a cron job with such searches, use a command like that to show a file in the /etc/cron daily directory. Make sure the output of these commands is redirected to an appropriate file, perhaps in the /var/log directory, suitable for later analysis.

Of course, Linux software comes in other formats. Software suitable for Red Hat distributions are downloaded as package files with .rpm extensions. In contrast, software packages for Debian-based distributions such as Ubuntu are available as package files with deb extensions.

# Executable Files

Naturally, users may set up their own executable files in their home directories. With allowed the chmod command. While a few executable files are necessary for certain applications, however, such files should be kept to a minimum. The find command can also be helpful in this area. For example, the following command searches for all files (-type f) with user, group, and other executable permissions, starting with the /home/ directory:

```
# find /home/ -type f -perm /u=x,g=x,o=x
```

Unfortunately, the abilities of this command are limited, especially with respect to applications such as the Evolution Personal Information Manager. Many Evolution data files have to executable permissions.

Perhaps as dangerous as executable files they are with Set User ID (SUID), Set Group ID (SGID), and sticky-bit permissions. Once created by a user, a black hacker may manage arrange to have them run by a user associated with a service, potentially infecting that with malware of some sort. The find command can be used to search for files with the following command:

```
# find /home/ -type f -perm /u=s,g=s,o=t
```

While changes in executable-permissions are tracked by tools as Tripwire and AIDE in a system, they might not be tracked in user home directories. There are legitimate uses for executable scripts. For example, engineers might have big database jobs that want to run at night through the cron daemon. The tracking of executable files in directories is often left to customized searches with the find command.