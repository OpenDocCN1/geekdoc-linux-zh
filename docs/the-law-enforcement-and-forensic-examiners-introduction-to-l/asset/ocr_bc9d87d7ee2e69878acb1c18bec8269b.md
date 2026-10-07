# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

We then use icat to recover the file. In this case, we just pipe the first few lines out to see our string of interest, cybernetik.

```
barry@forensic1:~/2$ icat -o 10260 able2.bd 10090 | head -n 10 //
* fixer.c
* ByIdex
* inspired on sum.c and SaintStat 2.0
* updated by Cybernetik for linux rootkit
*/
```

```
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/time.h>
```

# Sleuth Kit Exercise #4 – NTFS Examination: File Analysis

At this point we've done a couple of intermediate exercises using ext2 and ext4 file systems from a Linux disk images. In the following exercises we will do some analyses on an NTFS file system. This is the most common file system likely to find when it comes to personal desktop and laptop computers today.

Some might ask, "why?” There are many tools capable of analyzing NTFS file system in its native environment. In my mind there are two very good reasons for reason to apply the Sleuth Kit on Windows file systems. First, the Sleuth Kit is comprised of a number of separate tools that have to work with discrete sets of capabilities. The specialized nature of these tools means that you have to understand their interaction with the file system being analyzed. This makes them es suited to help learning the ins and outs of file behavior. The fact that the Sleuth Kit does less of the work for you makes it a great learning tool. Second, an open source tool that operates in an environment other than Windows makes for an excellent cross-verification utility.

The following exercise follows a set of basic steps useful in most any analysis. Make sure you follow along at the command line. Experimentation is the best way to learn.

If you have not already done, I would strongly suggest (again) that you invest in a copy of Carrier's book: File System Forensic Analysis (Published by Addison-Wesley, 2005). This book is the definitive guide to file behavior for forensic analysts. As a reminder (again), the purpose of these exercises in NOT to teach you file systems (or forensic methods, for that matter), but rather to illustrate and introduce the detailed information TSK can provide on file systems encountered by field examiners.

For these exercises that follow, we will be using the NTFS_Pract_2017.E01 set of files we downloaded and used for our libwf sections earlier. Since these are EWF files, and we have

242