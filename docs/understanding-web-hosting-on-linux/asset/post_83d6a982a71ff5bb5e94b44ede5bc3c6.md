
(close the window or type exit at the command line) and fire up your browser (which we assume is Netscape. Enter that address into the Location field and press Enter. You will be prompted to log into Webmin.)

It is important to note that the user name and password you use to log into Webmin will determine the level of access you are granted. Webmin honors Linux privileges, so log as the root user. You should find yourself at the screen shown in Figure 10.3.

![](img/069cd06404ac5e90171e6d857bf3ad28_165_0.png)

The very first task to perform is to verify that you have Webmin secured from the world. Upon initial installation, it should be configured to accept connections only from the loopback interface, meaning that you can connect to it from your local machine (localhost) on IP address 127.0.0.1. You want to ensure that this is the case. If you were to log into Webmin from another machine on an unencrypted connection, the user name and password would travel the network in plain text, so that anyone with a packet sniffer would be able to configure your system for you very quickly. That would be a bad thing.

To verify that Webmin is listening on the loopback interface only, click the Webmin Configuration link, and then click Ports and Addresses. If the resulting display resembles Figure 10.4, you are ready to go. If it doesn't, make it do so, and then click Save.

## Linux Operation, Configuration, and Administration — 151

![](img/069cd06404ac5e90171e6d857bf3ad28_166_0.png)

Figure 10.4: This screen shows Webmin listening on the loopback interface only.

To further increase your protection, click IP Access Control and make the adjustments in your browser window until you have configured as shown in Figure 10.5. This tells Webmin to accept connections only if they come from 127.0.0.1, which is the local loopback address. In other words, you can only access Webmin from the same machine it is running, so you are doubly protected if you accidentally expose Webmin to connections from the network.

![](img/069cd06404ac5e90171e6d857bf3ad28_166_1.png)

Figure 10.5: For added security, configure IP Access Control as shown here.

If you want or need to configure your system from another machine, configure Webmin using an encrypted link. That is beyond the scope of this book, but if the topic interests you, follow the SSL Encryption link on the Webmin configuration page...

## File System Administration

Under normal circumstances, you will have little to do with file system administration. Linux systems, and servers in particular, run for months or even years without a reboot. Given that reliability, there are only three situations where you will need to worry about your file system:

- 1. You turn your computer off without issuing the shutdown command or the power goes off and you don't have a suitable uninterruptible power supply (UPS).
- 2. One or more of your partitions run out of space.
- 3. Your hard drive fails.

The lack of a proper file system is a very bad idea. The lack of a UPS is a stupid idea for a Web server. Linux, like most current operating systems, use memory as a cache (temporary storage) for data that is coming from going to the disk drive. The premise is: as fast drives have become, accessing data from them is still tremendously slower than a comparable data exchange from memory. So, the operating system will store changes in memory until a convenient time becomes available to flush the cache to disk. The result is a system that is more responsive to the user, or in the case of a Web server, quicker response times. The trade-off is certain exposure to the possibility that the system could die before the changes get written to disk. Rudely shutting down the computer is a glaring example of that. The best-case scenario is an extended boot time while a file system check is done (which will be explained shortly). The worst-case scenario is a loss of data, with an unbootable or unusable system.

> Note: Never power your system with the power switch; use shutdown -h now. Systems without power management can be turned off using the switch once the "power off" message appears on the screen.

And, for crying out, buy a UPS! (Preferably one with a communications port for the computer—Linux can monitor for a lack of commercial power and shut itself down and cleanly.)

If you manage to shut down your Linux system abruptly, you will be introduced to the file system check (fsck). Linux will automatically run fsck if it finds that the partition was not cleanly unmounted during the prior shutdown (because you turned off the power). This is where you will be punished for your mistake, an fsck on a large partition can last quite some time. And since each one of your partitions is in the same time, you'll get to check each partition being cleaned. (Either, or you can start ten-page paper by being putting off.) Most of the time, you'll see a bunch of messages listing the things that are being fixed and, if the stores are aligned properly, you'll get a "successful" message at the end of each partition. If not, you'll have to run fsck by hand. If this is the case, Linux will let you guide you through the process.

Various journaling file systems are under development to help alleviate the trauma to file systems if you lose power, but to avoid this situation. One other thing about fsck: it runs automatically n times you reboot your computer (where n is some number that you can change with the tune2fs command) or when it has been a long time between restarts. Don't assume, therefore, that you had a power drop just because fsck ran during a boot.

## Linux Operation, Configuration, and Administration • 153

The second "oops" in list is running out of space in a partition. This can have some interesting side effects. Assuming that it's not your root partition that has become full, the unusual symptom is that your servers shut down or refuse to accept connections. If this ever happens, one of the first things you should check is that you still have some disk space available. One way is to use Webmin at http://localhost:10000 and sign on. Click the Hardware tab, and then click Partitions on Local Disk. On the right side of the screen, you'll see a list of all your partitions and a percentage of the space still available. If any partition shows zero, you've found the problem.

You might be wondering, "If my system is not accepting connections, how can I connect to Webmin?" Good question! The answer is that you might not be able to connect. In that case, you'll have to fall back to Plan B, which is to open a terminal session (use Ctrl-Alt-F2 and sign on) use the df command, which is the tried-and-true Linux way to get the same data. There is one caveat: though the percentage of the disk space used, which is just the opposite of Webmin. In this case, you're looking for a partition that's 100 percent used.

In either case, you have some housekeeping to do. The first thing you need to do is find where your space is going, by using the du command. Change the mount point on the offending partition and issue the following to get a list of the directories and their sizes, in descending order of size:

```
du -x | sort -gr | more
```

You can use the command to figure out each of these switches does. Once you've identified which directories the drive-space hogs, examine each one and delete unnecessary files, such as your MP3 material that you downloaded.

If, after all of your housekeeping efforts, you still can't find enough room to run, your next solution is: recreate your partitioning scheme. Perhaps you can run Peter to pay Paul by taking space from one partition and assigning it to another. Use one of the various tools available for this task, like the commercial product or the open-source program. If that isn't possible, you'll need to purchase and install another disk drive. (The steps implemented with each partitioning or disk installation are outside the scope of this book.)

The third pitfall, hard drive failure, is the least likely because of the reliability of the current generation of hard drives. When it occurs, however, the solution is straightforward: buy a new drive and restore your system from your last backup. Sometimes you can get lucky with a failed drive and be able to extract information from it, but don't press luck. A disk drive is able to heal itself, so when it starts to go, put it out to pasture. (Backups are discussed later in this chapter.)

## Facility Monitoring

One of the most important functions of a system administrator is to maintain a vigil on the system to ensure everything is going fine. Webmin provides the access to the information you need. Point your browser to your system, and click the System tab, choose System Logs. To view a log, click the activated on the right side of the screen. Although you won't need to do it, you can configure the logging function using the left at of the screen.

Two of the logs are of particular interest. First, /var/log/messages, is where all system daemon-logging takes place. When that disk drive starts to act flaky or a daemon is configured incorrectly, you'll probably find suspicious messages here. The second log, /var/log/secure, is where all
