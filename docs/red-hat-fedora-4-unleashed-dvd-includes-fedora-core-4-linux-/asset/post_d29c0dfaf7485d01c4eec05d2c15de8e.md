
![](img/774d40fd20903495c5cd00e2efad3f33_448_0.png)

FIGURE 15.3 The Process Listing view of the System Monitor.

Choose Hidden Processes under the Edit command accessible from the top of the display to show any hidden processes (those that the kernel does not enable the normal monitoring tools to see). Select any process and kill it with End Process.

The processes can be re-niced by selecting Edit, Change Priority. The View selection from the menu bar also provides a memory map. In the Resource Monitor tab, you can view a moving graph representing CPU and memory usage (see Figure 15.4).

## KDE Process and System Monitoring Tools

KDE provides several process and system monitoring clients. The KDE graphical clients are integrated into the desktop taskbar by right-clicking on the taskbar and following the menus.

These KDE monitoring clients include the following:

- **kdf**—A graphical interface to your system's filesystem table that displays free disk space and enables you to mount and unmount filesystems using a pointing device.
- **ksysguard**—Another panel applet that provides CPU load and memory use information in animated graphs.

![](img/774d40fd20903495c5cd00e2efad3f33_449_0.png)

FIGURE 15.4 The Graph view of the System Monitor. It shows CPU usage, Memory/Swap usage, and disk usage. To get this view, select the Resource Monitor tab.

## Reference

- http://and.sourceforge.net/—Home page of the and auto nice daemon, which can be used to prioritize and reschedule processes automatically.
- http://sourceforge.net/projects/schedutils/—Home page for various projects offering scheduling utilities for real-time scheduling.
- http://freetype.sourceforge.net/patents.html—A discussion of the FreeType bytecode interpreter patents.
- http://www.etheral.com—Home page for the Ethereal client.
- http://www.realvnc.com/—The home page for the Virtual Network Computing remote desktop software, available for a variety of platforms, including Fedora Core Linux. This software has become so popular that it is now included with nearly every Linux distribution.

# CHAPTER 16
## Backing Up, Restoring, and Recovery

This chapter examines the practice of safeguarding data through backups, restoring that same data if necessary, and recovering data in case of a catastrophic hardware or software failure. After reading this chapter, you will have a full understanding of the reasons for sound backup practices. You can use the information in this chapter to make intelligent choices about which strategies are best for you. The chapter also shows you how to perform some types of data recovery and system restoration on your own and when to seek professional assistance.

## Choosing a Backup Strategy

Backups are always trade-offs. Any backup will consume time, money, and effort on an ongoing basis; backups must be monitored, validated, indexed, stored, and new media continuously purchased. Sound expensive? The cost of not having backups is the loss of your critical data. Re-creating the data from scratch will cost time and money, and if the cost of doing it all again is greater than the cost associated with backing up, you should be performing backups. At the where-the-rubber-meets-the-road level, backups are nothing more than insurance against financial loss for you or your business.

Your first step in formulating and learning to use an effective backup strategy is to choose the strategy that is right for you. First, you must understand some of the most common (and not so common) causes of data loss so that you are better able to understand the threats your system faces. Then, you need to assess your own system, how it is used and by whom, your available hardware and software resources, and your budget constraints. The following sections look at each of these issues in detail, as well as offering some sample backup systems and discussing their use.

### IN THIS CHAPTER

- Choosing a Backup Strategy
- Choosing Backup Hardware and Media
- Using Backup Software
- Copying Files
- Undeleting Files
- System Rescue
- Reference

### Why Data Loss Occurs

Files disappear for any number of reasons: They can be lost because the hardware fails and causes data loss; your attention might wander and you accidentally delete or over-write a file. Some data loss occurs as a result of natural disasters and other circumstances beyond your control. A tornado, flood, or earthquake could strike, the water pipes could burst, or the building could catch on fire. Your data, as well as the hardware, would likely be destroyed in such a disaster. A disgruntled employee might destroy files or hardware in an attempt at retribution. And any equipment might fail, and it all will fail at some time—most likely when it is extremely important for it not to fail.

#### A Case in Point

A recent Harris poll of Fortune 500 executives found that roughly two-thirds of them had problems with their backups and disaster-recovery plans. How about you?

Data can also be lost because of malfunctions that corrupt the data as it attempts to write to the disk. Other applications, utilities, and drivers might be poorly written, buggy (the phrase most often heard is “still beta quality”), or might suffer some corruption and fail to correctly write that all-important data you have just created. If that happened, the contents of your data file would be indecipherable garbage of no use to anyone.

All of these accidents and disasters offer important reasons for having a good backup strategy; however, the most frequent cause of data loss is human error. Who among us has not overwritten a new file with an older version or unintentionally deleted a needed file? This applies not only to data files, but also to configuration files and binaries. While perusing the mail lists or the Usenet newsgroup postings, stories about deleting entire directories such as /home, /usr, or /lib seem all too common. Incorrectly changing a configuration file and not saving the original in case it has to be restored (which it does more often than not because the person reconfigured it incorrectly) is another common error.

### TIP

To make a backup of a configuration file you are about to edit, use the `cp` command:

```bash
$ cp filename filename.original
```

And to restore it:

```bash
$ cp filename.original filename
```

Never edit or move the *.original file, or the original copy will be lost. If it is, you can extract the configuration files from an .rpm file to at least provide the out-of-the-box configuration; Chapter 7, “Managing Software and System Resources,” explains how to do that.

Proper backups can help you recover from these problems with a minimum of hassle, but you have to put in the effort to keep backups current, verify their intactness, and practice restoring the data in different disaster scenarios.

### Assessing Your Backup Needs and Resources

By now you have realized that some kind of plan is needed to safeguard your data, and, like most people, you are overwhelmed by the prospect. Entire books, as well as countless articles and whitepapers, have been written on the subject of backing up and restoring data. What makes the topic so complex is that each solution is truly individual.

Yet, the proper approach to making the decision is very straightforward. You start the process by asking:

- What data must be safeguarded?
- How often does the data change?

The answers to these two questions determine how important the data is, determine the volume of the data, and determine the frequency of the backups. This in turn will determine the backup medium. Only then can the software be selected that will accommodate all these considerations. (You learn about choosing backup software, hardware, and media later in this chapter.)

Available resources are another important consideration when selecting a backup strategy. Backups require time, money, and personnel. Begin your planning activities by determining what limitations you face for all of these resources. Then, construct your plan to fit those limitations, or be prepared to justify the need for more resources with a careful assessment of both backup needs and costs.

> **TIP**
>
> If you are not willing or capable of assessing your backup needs and choosing a backup solution, there exists a legion of consultants, hardware vendors, and software vendors who would love to assist you. The best way to choose one in your area is to query other Unix and Linux system administrators (located through user groups, discussion groups, or mail lists) who are willing to share their experiences and make recommendations. If you cannot get a referral, ask the consultant for references and check them out.

Many people also fail to consider the element of time when formulating their plan. Some backup devices are faster than others, and some recovery methods are faster than others. You need to consider that when making choices.

It is a good idea to examine incidents of data loss in the past and decide if your chosen scheme will adequately address that loss. Finally, examine what effect a total disaster might have. In each case, ask yourself: What data am I protecting? How will it be safe? How will it be restored, and how long will that take? The answers to all these questions should help you form your plan.
