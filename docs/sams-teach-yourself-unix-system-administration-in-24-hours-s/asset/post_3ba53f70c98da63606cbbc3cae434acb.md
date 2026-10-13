
As you can see, to set a specific account expiration date, you need to use the Solaris usermod command, with a -e flag. To accomplish the same task as shown in Linux with the chage command, therefore, requires two steps:

```
# passwd -x 30 -w 2 testdude
# usermod -e 08/03/2003 testdude
```

Notice that there's no way to automatically lock accounts after a certain number of days of inactivity (the -I flag in the Linux chage command).

Checking the settings is yet another Solaris command: logins. There are lots of flags to this useful utility (see the man page for details), but to see the settings for a specific account, use the -x extended output flag:

```
# logins -x testdude
testdude 102 other 1
/home/testdude
/bin/sh
NP 011802 0 30 2
```

The output is a bit cryptic, but remember that NP means "no password," and much of the rest of the information can be inferred by peeking at the /etc/passwd entry:

```
# grep testdude /etc/passwd
testdude:x:102:::/home/testdude:/bin/sh
```

The output of logins shows us that account testdude has UID 102, and a default group of other, which has a GID of 1. The home directory is /home/testdude, the login shell is /bin/sh, and the password expiration information is, in order: date the password last changed, number of days required between changes, number of days allowed before a change is required, and the pre-expiration warning value.

Do you see what's missing? There's no clue that the account itself is scheduled to automatically turn off in August of 2003.

Linux offers a succinct and sophisticated password aging capability through its chage command. Solaris offers a similar capability, but the interface is considerably more awkward, split across three different commands. And Darwin—well, as of yet, Darwin doesn't support password aging.

Regardless of whether it's easy or difficult, however, the password aging capability is a very good addition to your Unix sysadmin toolkit if it's available on the systems you administer.

## Summary

This hour has explored many facets of account management, with a focus on working with recalcitrant users and shutting them down as needed. It also highlights how much difference there can be between different flavors of Unix. Just because they all have the same OS name doesn't mean that they're identical!

## Q&A

Q Why is it so important to make sure that someone isn't logged in if you're going to disable their account?

A Oftentimes you'll find that you need to suspend an account because of inappropriate activity by the user, or because the user's been furloughed temporarily. In those situations, it's best to avoid any potential copying of confidential files, attempts to sabotage the system, or what have you by simply giving the user the boot.

Q The whole idea of file locking seems pretty critical to the design of a multiuser operating system. Is it?

A Absolutely, and even with file locking, it's still not uncommon for multiple admins to override each others' changes (what I'd call "stepping on each other"). The best policy is to have one person who is empowered to make changes to critical files, then let everyone else feed change requests to them.

## Workshop

## Quiz

- 1. What's the super-fast less-than-a-minute technique for suspending a user account?
- 2. The passwd command on most Unix systems has heuristics (a fancy word for rules) defining what is an acceptable password. Find out what the rules are on your main system.
- 3. The built-in usermod -L mechanism for locking accounts consists of simply sticking an ! in front of the encrypted password string. Will that work for any system? Try it.
- 4. Why might you use passwd -d on a Linux or Solaris system?

## Answers

- 1. Suspending a user account can be done very quickly by changing the password as root.
- 2. The easiest way to find out what rules the passwd command uses is to check the passwd man page. Here's the relevant excerpt from the Solaris man page:

Passwords must be constructed to meet the following requirements:

- Each password must have PASSLENGTH characters, where PASSLENGTH is defined in /etc/default/passwd and is set to 6. Only the first eight characters are significant.
- Each password must contain at least two alphabetic characters and at least one numeric or special character. In this case, "alphabetic" refers to all upper or lower case letters.
- Each password must differ from the user's login name and any reverse or circular shift of that login name. For comparison purposes, an upper case letter and its corresponding lower case letter are equivalent.
- New passwords must differ from the old by at least three characters. For comparison purposes, an upper case letter and its corresponding lower case letter are equivalent.
- 3. Prefacing an encrypted password string with a new character will definitely make the password unmatchable, effectively turning the account off. It's another trick you can use if there's no locking mechanism available.
- 4. If you set up an account with a shell of, say, lpq or something similar, you might make it general access by informing users that they can log in to the lpq account from any login prompt to see the state of the printer queue.

In the next hour, we'll have a close look at backup and archiving tools with Unix, focusing specifically on gzip and tar, two tools that every Unix system administrator should know like the proverbial back of the hand. We'll also compare compression packages to see which does the best job of saving disk space and making transfers more speedy.

![](img/5ced0c78d748bd190e9027e5549a3622_149_0.png)

## Hour 7

## Large File Management and Backups

The last few hours have concentrated on tools and techniques for managing user accounts on your Unix system. However, users have expectations of you as a system administrator in much the same way you have expectations of them. Chief among their expectations is that the file system has a high level of integrity. Put another way, you'd better be doing backups!

This hour will concentrate on managing large files and archives, and then talk about common methods of backing data up onto an archival device.

In this hour you'll learn about

- Managing big files with compress
- The gzip alternative
- A zippy tour of zip
- Copying directory trees with tar
- Dump and system backups

## Shrinking Big Files with compress

If you've picked up the newspaper in the last few years or walked into a computer shop, you know that the price of hard disks has been decreasing at a rather astonishing rate. Today I can walk into the local electronics store and buy a 40 gigabyte hard disk for under $100. When I remember how much my first 20 megabyte disk cost years ago... well, I promised I wouldn't bore you with reminisces, so I'll stop there.

The point is that it's hard to imagine filling up disks, or having files on a Unix system that are so large that it's necessary to worry about coming up with a technique that will let you shrink them down.

Until, that is, your users start to explore multimedia files. A four minute MP3-encoded music file can easily be 50MB or more, a JPEG image from a digital camera can sprawl across 1MB or more, and even Word documents have been known to grow at a surprising rate once editing and reviewing begins.

That's why one of the foundational topics for system administration is managing large files. Like it or not, you have some on your computer, and you're bound to have more as more users are added (or as you use it more yourself).

## Task 7.1: Working with compress

The primary cross-platform tool for managing large files is a program called compress, which uses an adaptive Lempel-Ziv encoding that shrinks files down 20% to 30% on average.

- 1. To start out, I've been exploring how my users are using their disk space, and found that that pesky taylor guy has all sorts of large files in his directory. Here's a representative sampling:

```
$ ls -l
total 5036
-rw-r--r-- 1 taylor coders 1113 Jan 10 08:12 adduser.sh
-rw-r--r-- 1 taylor coders 56 Dec 5 05:10 badjoke
-rw-r--r-- 1 taylor coders 56 Dec 5 05:10 badjoke.rot13
drwxrwxr-- 2 taylor coders 4096 Dec 5 05:48 bin/
-rw-r--r-- 1 taylor coders 739 Dec 5 05:11 browse.sh
-rw-r--r-- 1 taylor coders 276 Dec 5 05:11 buckaroo
drwxrwxr-x 2 taylor coders 4096 Dec 18 21:26 CBO_MAIL/
-rw-r--r-- 1 root coders 537 Jan 9 22:39 checkhomes.sh
-rw-r--r-- 1 root coders 756 Jan 14 21:31 checkpw.sh
drwxrwxr-- 2 taylor coders 4096 Dec 5 05:12 CraigsList/
-rw-r--r-- 1 root coders 693 Jan 14 06:40 delete.sh
drwxrwxr-- 4 taylor coders 4096 Jan 7 21:47 DEMO/
-rw-r--r-- 1 taylor coders 373 Jan 7 20:22 diskhogs.sh
drwxrwxr-- 2 taylor coders 4096 Dec 5 05:12 elance/
```

![](img/5ced0c78d748bd190e9027e5549a3622_150_0.png)
