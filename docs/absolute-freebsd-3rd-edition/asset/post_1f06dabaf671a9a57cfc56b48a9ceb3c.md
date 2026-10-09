
a file for later analysis:

```
# mtree -x -i -c -K sha512 -K sha256 -p / -X /home/mwlucas/mtree-exclude > /tmp/mtree.out
```

While you can use mtree(1) across the entire server, most people use -x 1 to run it once per partition. You don’t want to record checksums on frequently changing files, such as the database partition on your database server. Collecting checksums on NFS mounts has the twin features of running really slowly and increasing network congestion. The -ic flag 2 tells mtree to print its results to the screen, with each subsequent layer in the filesystem indented. This format matches the system mtree files in /etc/mtree. The -k flag accepts several optional keywords; in this case, we want to generate SHA512 checksums 3 and SHA256 checksums 4. The -p flag 5 tells mtree which partition to check. Almost every partition has files or directories that change on a regular basis and that you therefore don’t want to record checksums for. Use -x 6 to specify an exclusion file, a file containing a list of paths not to match. Finally, redirect the output of this command to the file /tmp/mtree.out 7.

### mtree(1) Output: The Spec File

mtree(1)’s output is known as a specification, or spec. While this specification was originally intended for use in installing software, we’re using it to verify a software install. Your spec starts with comments showing the user who ran the command, the machine the command ran on, the filesystem analyzed, and the date. The first real entry in the spec sets the defaults for this host and begins with /set.

```
/set type=file uid=0 gid=0 mode=0755 nlink=1 flags=uarcb
```

The mtree(1) program picked these settings as defaults based on its analysis of the files in the partition. The default filesystem object is a file, owned by UID 0 and GID 0, with permissions of 0755, with one hard link and the user archive flag. After that, every file and directory on the system has a separate entry. Here’s the entry for the root directory:

```
1.    2type=dir3nlink=194time=1504101311.033742000
```

This file is the dot (.) 1, or the directory we're in right now. It’s a directory 2, and it has 19 hard links 3 to it. This directory was modified 1,504,101,311.033742000 seconds into Unix epochal time 4. The Unix epoch began January 1, 1970.

### EPOCHAL SECONDS AND REAL DATES

Don’t feel like counting seconds since the epoch began? To convert epochal seconds into normal dates, run date -r seconds. Cut off the fraction at the end of mtree’s time, however; date(1) likes only whole seconds.

In some ways, the entry for the directory is rather boring. An intruder can’t realistically replace the directory itself, after all! Here’s an entry for an actual file in the root directory:

```
 .cshrc      mode=0644 nlink=21size=950 time=1499096179.000000000  
2 sha256digest=20d2a78c9773c159bac1df5585227c7b64b6aab6b77bccadbe4c65f1be474e8c
3
sha512=2d4d330e327f75f10101c dc7c0d6a5e916336ade5b9eb04b0d96ea43d221c5eac4c71a89dfe85a...
```

We see the filename and the same mode, link, and time information as in the root directory, but also get the file size 1. Additionally, there’s the SHA256 2 and SHA512 3 cryptographic hashes computed from the files.

While it’s theoretically possible for an intruder to craft a file that matches a particular cryptographic hash, and while cryptographers are constantly trying to find practical ways to create files that match arbitrary SHA256 and SHA512 checksums, it’s extremely unlikely that an intruder can create a fake file that matches both checksums, contains his backdoor, and still functions well enough that the system owner won’t immediately notice a problem. By the time this happens, we will have additional checksum algorithms resistant to those methods and will switch to them.

### The Exclusion File

The exclusion file (given with `-x`) lists filesystems you don’t want mtree(1) to analyze. Lots of filesystems will change without malicious intervention. Log files and user home directories should change. Directories like `/tmp` and `/var/db/entropy` *better* change on a functional system. List each directory you don’t want checked on its own line in the exclusion file, with a leading dot.

```
./tmp
./var/db/entropy
./var/log
./usr/home
```

Wait a day or so, and then run mtree(1) again to generate a new spec file. Differences between the two mtree files will let you improve your exclusion file. You’ll do the exact same thing when you suspect a system intrusion.

### Saving the Spec File

The spec file contains the information needed to verify the integrity of your system after a suspected intrusion. Leaving the spec file on the server you want to verify means that an intruder can edit the file and conceal his wrongdoing. You must not save the file on the system itself! Now and then someone will suggest that you checksum the mtree spec file but keep it on the server. That’s not useful; if someone tampers with the mtree file and the checksum, how would you know? Or worse—if someone tampered with the spec file and you caught it, you couldn’t tell what change had been made! Copy your spec file to a safe location, preferably on an offline media, such as a flash drive or an optical disk.

### Finding System Differences

When something raises your suspicions and you begin to think that you might have suffered an intrusion, create a new mtree spec file and compare it with the “known good” spec file you stored offline. Use mtree(1) to check for differences between spec files.

```
# mtree -f mtree.suspect -f mtree.good > mtree.differences
```

Every entry in the file is something that has changed. My exclusion file is finely tuned, eliminating files I expect to have changed. This particular run generates two lines of output.

```
bin/sh file¹size=161672
② sha256digest=a4a85ca3563d8f3bda449711c6b591b37093e668fc136f88282e9b188b955f56ab③
sha512=011793e3c6accd99b4261e0a0f3a0b9bd6a6842f3ccd55da1ce2070b568ec3c49ae7b0e51d33bb59eff...  
bin/sh file size=④10489808
⑤ sha256digest=45856525d4251b43d8df1429cfile0f4adb664f06df7f995aace5b7ca0c03c2⑥
sha512=a4f0e83e5fb12d615721fd7d57cb6a120068d1aa71fc305b7b86927391f33bec822cf14ce8a8a9db14...
```

The file /bin/sh ① has changed size ④ between mtree runs. This isn’t good. Also, note the two different SHA256 hashes ② ⑤ and the two different SHA512 hashes ③ ⑥. Don’t hit the panic button yet, but start asking your fellow sysadmins pointed, hard questions. If you can’t get a good answer as to why this binary changed, you might look for your installation media.

Or, perhaps you need to update your exclusion file. But if /bin/sh changed, probably not.

### Monitoring System Security

So, you think your server is secure. Maybe it is . . . for now.

Unfortunately, there's a class of intruders with nothing better to do than to keep up on the latest security holes and try them out on systems they think might be vulnerable. Even if you read *FreeBSD-security* religiously and apply every single patch, you still might get hacked one day. While there's no way to be absolutely sure you haven't been hacked, the following hints will help you find out when something does happen:

- Be familiar with your servers. Run `ps -axx` on them regularly, and learn what processes normally run on them. If you see a process you don't recognize, investigate.
- Examine your open network ports with `netstat -na` and `sockstat`. What TCP and UDP ports should your server be listening on? If you don't recognize an open port, investigate. Perhaps it's innocent, but it might be an intruder's backdoor.
- Unexplained system problems are hints. Many intruders are ham-fisted klutzies with poor sysadmin skills, who use click-and-drool attacks. They'll crash your system and think that they're the cyber incarnation of Samuel L. Jackson.
- Truly skilled intruders not only clean up after themselves but also ensure that the system has no problems that might alert you. Therefore, systems that are unusually stable are also suspicious.
- Unexplained reboots might indicate someone illicitly installing a new kernel. They might also be a sign of failing hardware or bad configuration, so investigate them anyway.
- FreeBSD sends you emails every day giving basic system status information. Read them. Save them. If something looks suspicious, investigate. Look at old messages to see when something has changed.

I particularly recommend the `lsof` package to increase your familiarity with your system. The `lsof` program lists all open files on your system. Reading `lsof(8)` output is an education in and of itself; you probably had no idea that your web server opened so much crud. Seeing
