
False positives and negatives are not limited to computing. Imagine the case in which a person goes to a doctor and gets an ultrasound scan. Based on the scan results, the doctor reports that the person has cancer. However, on further examination it appears that the initial report was incorrect. This is an example of a false positive. Although additional tests were unnecessarily performed based on the false positive, it is still much better than having a false negative, with the cancer going unnoticed and untreated.

Because Chkrootkit reports using tools on the computer, it may report a false negative. There are ways around this problem as described later in this section.

## 10.2.2 What If Chkrootkit Says the Computer Is Infected?

If Chkrootkit says your computer is infected, the first thing you should do is tell yourself to remain calm. Although you should not assume so, there is a chance that Chkrootkit is reporting a false positive. If Chkrootkit reports an infection, you should immediately take steps to mitigate any further damage.

The preceding chapter of the book looked at incident response. Therefore, it would be redundant to cover that same material in this chapter. However, as with all tools of this nature, false positives come with the territory. It's in your best interest to take the notice seriously, but it might also be wise to try to determine whether Chkrootkit has reported a false positive.

Chkrootkit uses various means to find rootkits. Many times Chkrootkit looks for a certain signature in a file based on a known trojaned version of the file. Other times Chkrootkit looks for ports that are open that have been known to be the result of a rootkit or other attack. This was the case for the report of infection highlighted earlier in this section. Chkrootkit reported that it believed that the computer was infected with the bindshell rootkit. It based this finding on two ports that it found open, 1524 and 31337. In reality, these ports were open because of another security tool, PortSentry, that listens on those ports in hopes of catching other infected hosts. I used the program `lsof` with the `-i` option to determine the exact program that was listening on those ports.

With more than 50 rootkits reported by Chkrootkit, you probably won't know the exact ramifications of being infected by a given rootkit. Further, there's a good chance that if one rootkit has been run, multiple rootkits have been run, making cleanup all that much more difficult. To begin the process of damage control, you can search the web for each individual rootkit to determine what actions it takes when it's run. However, realize that, by definition, after a rootkit has been run successfully, the attacker has root privileges on the computer and therefore may have done much greater damage to the system or may be in the process of doing so now!

Whenever Chkrootkit reports an infection, you should take it seriously and always assume the worst. Prudence suggests that you should immediately unplug the computer from the network and take steps to clean up from the rootkit. In reality, it's rarely that easy or cut-and-dried.

## 10.2.3 Limitations of Chkrootkit and Similar Tools

Chkrootkit is a powerful and incredibly helpful tool but it is not without limitations. These limitations aren't really specific to Chkrootkit but rather are a limitation of any tool that attempts to perform complex checks such as this. One such limitation, false positives, has already been discussed. Another limitation of Chkrootkit and other tools like it is that they rely, by default, on programs included with the Linux computer itself, programs that may have been compromised or altered to avoid detection by prying eyes such as those of Chkrootkit and related utilities.

Here's a list of programs that Chkrootkit uses; keep in mind that these programs may themselves in turn rely on libraries or other things on the Linux computer that also may be compromised:

- awk
- cut
- echo
- egrep
- find
- head
- id
- ls
- netstat
- ps
- sed
- strings
- uname

Another limitation of tools such as Chkrootkit and shared by similar tools is that it can detect only rootkits that have been reported and for which it has been configured. Some unlucky soul has to be the first to have the rootkit run on her computer. If you happen to be that person, Chkrootkit won't help. Realize, though, that there is a fair chance that multiple rootkits will be run on the computer, which will make detection easier. I realize that this is small consolation.

## 10.2.4 Using Chkrootkit Securely

It's a good idea to use known-good sets of system binaries when using a tool such as Chkrootkit. Many rootkits replace vital system binaries such as `/bin/ps` with versions of their own. Therefore, if you try to use `ps` to find unknown processes, you may not be able to see them because the trojaned version of `ps` hides them.

Chkrootkit gives two methods for working around this problem. The first method involves using a known-good set of binaries, probably mounted from a CD-ROM. The second method involves physically mounting the possibly compromised hard drive into a different computer and then running the check from there. This second method is more appropriate for forensics after a successful attack rather than for investigating a possible attack.

Mounting a CD-ROM with known-good versions of binaries is a safe and easy method for performing a thorough examination using Chkrootkit. This method assumes that you have a CD-ROM with the correct binaries already on the disc. To run Chkrootkit with a CD-ROM copy of the binaries, first mount the CD. This is usually accomplished using the `mount` command, although sometimes it's mounted automatically. A common method for mounting the CD-ROM drive in most modern Linux distributions is shown here:

```bash
mount -t iso9660 /dev/cdrom /mnt/cdrom
```

Chkrootkit uses the `-p` option to define the location of the binaries it should use. Therefore, if the CD-ROM is mounted at `/mnt/cdrom`, you'd run Chkrootkit like so:

```bash
./chkrootkit -p /mnt/cdrom
```

The other method for running Chkrootkit is to physically mount the possibly compromised hard drive into another computer and run Chkrootkit against the contents of that drive. This is accomplished by specifying an alternate "root" directory for Chkrootkit. Assume that the second drive is mounted at `/mnt/drive2`:

```bash
./chkrootkit -r /mnt/drive2
```

## 10.2.5 When Should Chkrootkit Be Run?

Chkrootkit should be run whenever you'd like. There is no recommended schedule for Chkrootkit. I personally run it at irregular intervals for fun, but then again I'm just that type of guy. You should most definitely run Chkrootkit anytime you observe any suspicious activity on the computer or on other computers that may interact with or reside on the same network block as the computer in question. Whenever you run Chkrootkit, you should always hop out to the website, http://www.chkrootkit.org/, to check for a new version of the tool. A new signature for a rootkit or additional functionality might have been added since the version you're using.

You can also run Chkrootkit nightly from cron. However, I wouldn't rely on such a report being entirely accurate, but it could provide an early warning of an anomaly that needs your attention. Running Chkrootkit from cron might look like this:

```bash
0 4 * * * /path/to/chkrootkit
```

The cron entry shown will run Chkrootkit every morning at 4:00 a.m. Root (the recipient of cron job output) will receive a report every morning detailing the run of Chkrootkit.

## 10.3 Filesystem Integrity

Hand in hand with a rootkit checker such as Chkrootkit goes filesystem integrity software. Filesystem integrity software monitors important files on the computer and generates reports based on changes to those files. The administrator can then watch for unexpected changes to the files in question. For example, if files such as `/etc/resolv.conf` or even `/etc/shadow` change with no apparent reason, the administrator can take action.

Two popular filesystem integrity tools are Tripwire and AIDE. Tripwire had been the choice among administrators for a long time. However, Tripwire’s license changed, thus making commercial uses of the software questionable and even making the open-source nature of the software questionable. AIDE was developed as an alternative. In the meantime, the Tripwire license changed back, so as of this writing Tripwire is again a traditional open-source package. However, I’m not going to cover Tripwire in this book due to the license changes. I don’t want to have the license change yet again between the time I write this and the time you read it.

## 10.4 Log Monitoring

Monitoring log files is used to watch for anomalies that might indicate an attack. Although this method is used successfully, it can result in huge amounts of data and become cumbersome on large networks.

When combined with other tools, log monitoring can be made to work. For example, using log monitoring on a few key systems can reduce the amount of data being received. However, this and other such measures are really stop-gap measures because they do little to ensure the security of the systems that aren’t monitored.

Numerous packages are available to monitor log files. Three such packages include Logsnarter, Swatch, and Logcheck. More information on each can be found at their respective websites or from within your system’s documentation if the distribution includes them as available packages. I’ll briefly cover Swatch here just to give you a taste of some of the capabilities of these types of tools.

### 10.4.1 Swatch

Swatch is available with many Linux distributions as an add-on package or can be downloaded from http://swatch.sourceforge.net/. Swatch is highly configurable and can perform a number of actions based on a match.

Swatch works in several modes, including a mode called single-pass, which has the program parse a log file once, searching for matches and taking action based on those matches. Another mode sees Swatch perform a running tail (`tail -f`) of a log file looking for matches. By default, Swatch monitors `/var/log/messages` but it can be configured to monitor any file or even a socket.

Because Swatch is so powerful, I don’t feel as though I can do it justice in a book on Linux firewalls. I invite you to read more about Swatch. For now, I’ll give a recipe for monitoring.
