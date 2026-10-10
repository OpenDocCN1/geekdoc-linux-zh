
You may want to go through the main program storage directories (/usr/local/bin, /usr/local/sbin, and /usr/X11R6/bin) and check the status of every program. You can use pkg_info to determine what package owns a file, thus:

```bash
$ pkg_info -W /usr/X11R6/bin/xwave
/usr/X11R6/bin/xwave was installed by package xwave-2.2
$ pkg_info xwave-2.2
Information for xwave-2.2:

Comment:
Audio player/recorder/editor for the X Window System
```

**Note** *Some program files, particularly in the /bin, /sbin, /usr/bin, and /usr/sbin directories, don’t appear in the FreeBSD package database. Such programs were installed as part of the base FreeBSD system or by compiling a program from source code without the benefit of the FreeBSD ports system. You’ll have to evaluate these programs in other ways.*

The second `pkg_info` command in the preceding example returns additional information you can use to evaluate whether or not you really need the program installed on the computer. If you don’t, remove the program by using `pkg_delete`, as described further in Chapter 11:

```bash
# pkg_delete xwave-2.2
```

Although going through these directories shouldn’t be necessary very frequently, doing so isn’t a bad idea once you’ve become familiar with FreeBSD, in order to help identify and clean out unnecessary programs.

## Keeping a Tab on Users’ Files

Users sometimes consume excessive amounts of disk space. You can check on individual users’ disk space usage with the `du` command, which displays the disk space consumed by every subdirectory of the one you specify. To learn how much disk space is used in a particular directory and all its subdirectories, add the `-s` option. For instance, to learn how much disk space `sskinner` is using, type the command:

```bash
# du -s /home/sskinner
61034      /home/sskinner
```

![](img/f34d37e3abe9f4517128e54f80ab2616_716_0.png)

This output indicates that *sskinner*’s home directory contains 61,034 blocks of files. On most FreeBSD systems, each block is 1KB in size, so this value works out to 61,034KB. You can use this command to track who’s using how much disk space.

> **Caution**
> If your system’s permissions enable users to store files in common areas, tracking who disk space usage may be tricky or impossible with *du* alone, although you can use *du* to find out how much space is consumed by the common file areas.

On small systems, using *du* to track users’ disk usage can be reasonable; but on large systems, using *du* in this way can be quite tedious. For such systems, FreeBSD supports a feature known as *quotas* that enables FreeBSD itself to track users’ disk usage, and to block creation of files beyond a limit you specify. This feature can be quite worthwhile when you have many users, but you must enable it. This process can be a bit tedious, and some of the specific tasks have been covered in earlier chapters. In brief, enabling quotas requires performing these steps:

1.  **Compile quota support into the kernel**
    The standard FreeBSD kernel doesn’t ship with quota support. You must recompile your kernel, as described in Chapter 12, but add the *options QUOTA* line to the kernel configuration file. You must then recompile the kernel.

2.  **Enable quota support at boot time**
    Add the following lines to the `/etc/rc.conf` file to tell the system to use the newly-compiled quota support:
    ```bash
    enable_quotas="YES"
    check_quotas="NO"
    ```

    > **Note**
    > The *check_quotas* line tells FreeBSD whether or not to perform checks of quota consistency at boot time. This check can be lengthy, so it’s usually disabled by default; but you can enable it by setting the value to *YES* if you prefer.

3.  **Mount partitions with quota support**
    In `/etc/fstab`, you must add the *userquota* option to each filesystem you want mounted with user quota support, and *groupquota* to each filesystem in which you want to use group quotas. For instance, you might mount a `/home` filesystem using an entry such as this:
    ```text
    /dev/ada0s3h /home ufs rw,userquota,groupquota 2 2
    ```

4.  **Build quota databases**
    Type `quotacheck -a` to build the low-level quota databases on your quota-enabled filesystems.

5.  **Start quota support**
    Type `quotaon -a` to tell FreeBSD to begin using quotas for all the quota-enabled filesystems.

6.  **Edit a typical user's quota settings**
    Type `edquota -u username` to edit the quotas associated with *username*, or `edquota -g groupname` to edit quotas for the specified group. FreeBSD launches the editor specified by the EDITOR environment variable on a temporary file that specifies the user's quotas. You can then set the *hard limit*, which is the maximum disk space the user may consume; and the *soft limit*, which is the maximum disk space the user may consume over a long period. Both values are specified in blocks, which are usually 1024 bytes in size. For instance, if the hard limit is 100000 and the soft limit is 75000, the user may permanently store up to 75,000 blocks of files, and may temporarily exceed that limit to store up to 100,000 blocks of files. Precisely what "temporarily" means is defined in the kernel source code, or you can add `-t` to the edquota command to set the value you want. In addition to disk space, you can edit the number of *inodes* a user may consume. An inode is a data structure associated with a file, so the inode limit effectively caps the number of files a user may create. The quota file you edit resembles the following; you edit the hard and soft limits for both blocks and inodes:

    ```text
    Quotas for user sskinner:
    /usr: blocks in use: 61034, limits (soft = 75000, hard = 100000)
    inodes in use: 6391, limits (soft = 7500, hard = 10000)
    ```

7.  **Duplicate your typical user's settings**
    Use the `-p` option to edquota to copy your quota limits to a range of users. For instance, `edquota -p sskinner 1001-9999` duplicates *sskinner*'s quota limits to all users with UIDs between 1001 and 9999.

8.  **Tweak quota settings for special cases**
    If some users require bigger quotas than others, you can adjust their settings by performing Step 6 (and perhaps Step 7) to set the unique users' quotas.

I recommend you perform some tests to check that quotas are functioning as expected. Create a test account and attempt to go over quota in that account (say, by copying many large files to the account). If this doesn't work, or if the limits aren't what you expect them to be, rereview the preceding steps to be sure you've done everything correctly.

## Monitoring CPU Use

CPU time is an odd resource. Some systems have far too much CPU power for their own good—for instance, a typical workstation used for word processing and other tasks for which the user is the bottleneck doesn't need anywhere near as much CPU power as a typical computer delivers in 2002. Other systems, though, are used in multuser environments or to perform very CPU-intensive tasks, such as ray-tracing animation, engineering simulations, or scientific data analysis. Such computers often don't have enough CPU power for their users' desires. On such computers (especially multiuser systems), you may need to carefully track CPU use. If too many CPU-intensive jobs are run, the computer may become extremely sluggish. Indeed, such problems occasionally occur even on single-user computers because programs sometimes hang in such a way that they continue to consume CPU time, even though they aren't doing anything and their windows may even have closed. Knowing how to track CPU use, identify when CPU use is excessive, prevent problems, and correct problems can be a valuable set of skills for any FreeBSD administrator.

### Tools for Checking CPU Use

One of the most basic tools for checking on CPU use is *uptime*. This program reports how long a system has been running, how many users are logged in, and three *load averages*, which are measures of demand for CPU time in the past minute, five minutes, and fifteen minutes. An example of this command in use is:

```bash
# uptime
10:53AM  up 1 day, 20:17, 2 users, load averages: 0.06, 0.02, 0.01
```

In this example, the load averages are 0.06 for the last minute, 0.02 for the last five minutes, and 0.01 for the last fifteen minutes. A load average of 1.00 means that demand for CPU time exactly matches available CPU time. You're likely to see a load average of 1.00 or very close to it when you run a CPU-intensive program on a single-user workstation with no other CPU-intensive programs running. If you run two CPU-intensive programs on that computer, the load average will rise above 1.00. When this happens, programs can't get all the CPU time they request, and their performance degrades. Thus, the optimal load average for a computer is 1.00.

> **Note**
> Most programs create brief spikes of heavy CPU use as they display windows, perform computations, and so on, then drop down to near nothing as they wait for user input or terminate. Thus, even if your CPU load is low, the computer can seem sluggish if the CPU is underpowered because these brief spikes of CPU use will last longer than they would on a faster CPU.

If you use *uptime* and see that the load average is high, you may want to get a better idea of what's chewing up CPU time. You can do this with the *top* command, which displays a list of programs ordered according to CPU use. The program updates this list every few seconds so that you can monitor changes in CPU use. Figure 28-1 shows *top* in action. The *%CPU* and *CPU* columns show two measures of CPU use, and *top* sorts according to the *%CPU* column. The *command* column provides the name of the program that's consuming CPU time. In Figure 28-1, the *x11amp* program is consuming close to half the CPU time, *Xvnc* is consuming about 10%, and the remaining programs are consuming trivial amounts of CPU time.
