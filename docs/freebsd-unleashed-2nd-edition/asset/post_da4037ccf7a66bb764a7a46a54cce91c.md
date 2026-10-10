
- Do install sudo (/usr/ports/security/sudo) and encourage its use. If you have to share administrative privileges with others, giving them access to sudo is an excellent way to limit their potential for damaging the system while enabling them to still effectively manage things. In fact, sudo is appropriate for *all* administrators on a system, including yourself. Never do anything as root if you can do it with sudo in a more restricted environment; an inadvertently trashed system teaches all good administrators to limit even their own power.

- Do use ntpd and ntpdate to synchronize your system's clock so that all the system logging and scheduled processes in FreeBSD that depend on the time being accurate can operate properly. You can do this by adding the following lines to /etc/rc.conf:

```
ntpd_enable="YES"
ntpd_flags="tick.usno.navy.mil"
xntpd_enable="YES"
```

You can use any NTP server you like for ntpdate, which runs at boot time and corrects any gross time discrepancies before other services have a chance to run. You should also create an /etc/ntp.conf file to control ntpd, which runs as a daemon and keeps your clock synchronized with the NTP server (or servers) on an ongoing basis. See man ntp.conf for details on creating that file.

- Do be nice to the FreeBSD committers. There are only 15 or so of them, and the responsibilities of the entire operating system rest largely on their shoulders (as opposed to the collective shoulders of thousands of independent developers and distributors of Linux, or the corporate shoulders of Microsoft). That's a lot of responsibility. Be a cooperative and supportive user.

- Do decide what kind of security model you're going to have. Do you trust all your users? If so, you can get away with leaving a lot of system-level resources viewable. This way, when you have permission-collision problems (such as Web applications that must store clear-text passwords or write to a world-writable directory), you won't have to worry as much. If you don't trust all your users, though, you'll have to be much more careful. However, it's always best when running a networked server to lock down as much external security as you can. Even if you trust your local users, as long as your machine is on the Internet, it will be interesting to those who would like to break into it. See Chapter 29 for a fuller discussion of security in a networked environment.

- Do subscribe to the appropriate mailing lists for your version of FreeBSD. Unquestionably, you should be on freebsd-security@freebsd.org if you're running a server; freebsd-ports@freebsd.org and freebsd-questions@freebsd.org are also useful. If you're tracking the STABLE or CURRENT sources, subscribe to freebsd-stable@freebsd.org or freebsd-current@freebsd.org accordingly.

- Do monitor the size of your log files. Apache’s `httpd-access.log` and `httpd-error.log` are notorious for eating up disk space if your Web server gets any kind of significant traffic. Use Apache’s built-in `rotatelogs` utility or run a cron job to flush the logs occasionally. If your `/var` partition fills up, your mail, databases, and runtime files will not work.

Also, do be sure to *read* your logs! The system isn’t just writing out all that data for its health. Well, it is, actually, but it only works if you pay attention to what the system has to say.

- Do fly the Daemon banner proudly!

### DON’T:

- Don’t use experimental features on a production server. This isn’t the place to try out new ideas such as Soft Updates and unsupported filesystem kernel modules. Try these things out on a cheaply built “hobbyist” machine or a mirrored “backup” server; then put them into practice only once you’re comfortable with their use.

Beware, however, that if your test environment is not absolutely identical to your live machine, you run the risk of software failing in the production environment even if it worked on the test bed.

- Don’t port-scan your server if you’re running PortSentry or another tool that blocks your route to the machine when it detects an intrusion coming from your IP address. You’ll lose connectivity until you find an alternate direction from which to reach your server and delete the “blackhole” route.

Try to be aware of any action or situation that might block remote access to your machine. If that happens, you’ll require physical access to the machine in order to restore remote access.

- Don’t use `shutdown` to drop to single-user mode (for high-privilege activities such as replacing the kernel) if you’re running with the `securelevel` setting at 1 or higher. Using `shutdown` won’t decrement the kernel security level. Instead, reboot the machine and enter **boot -s** at the loader prompt to boot into single-user mode. Simply exit the single-user shell to come back up the rest of the way. You must boot in to and exit from single-user mode at the physical console!

- Don’t get hung up on uptime. If a system has 350-day uptime, this means the system has been sitting unused in a closet for a year or has not been conscientiously upgraded to keep up with security bulletins. Nonstop uptime doesn’t make for such great bragging rights as one might think.

- Don’t forget to add yourself to the “wheel” group at installation time! Very little is more disheartening than building a new server, driving 50 miles to the co-location facility, locking the server in a cabinet, driving home, trying to log in, and discovering you can't get root access.

- Don't make a habit of using filenames with spaces in them. This can be done with backslashes in front of the spaces, as with any other special character (for example, My\ Document.txt). There's no guarantee, however, that software will handle the filenames properly. Most of the time, it will, but there's still no guarantee.

- Don't write Perl or shell scripts on a local Windows machine and then upload them in binary mode over FTP, rather than in ASCII mode. Binary mode does not provide proper translation of end-of-line characters, which occurs properly in ASCII mode. Although the body of the uploaded script might look perfectly fine, the return character at the end of the very first line (#!/usr/bin/perl) will be unrecognizable to the shell and cause the script to fail.

> **TIP**
>
> If you're having trouble with CGI programming and scripts that mysteriously fail after uploading, check the #!/usr/bin/perl script first; then make sure you're uploading in ASCII mode. Better yet, do your programming directly on the server. Excellent text-editing tools (such as `vim`, `pico`, `emacs`) are available for just that purpose.

## Performance Tuning

In its default, “out of the box” configuration, FreeBSD is optimized to work with low-end hardware and to be extremely safe and reliable. This means that under heavy demand load, the system in its default state will perform more poorly than similarly equipped Linux or Windows servers. FreeBSD isn't an inferior platform; quite the contrary. Rather, it simply needs to be tuned for high-performance operation. The other platforms to which it's compared tend to be optimized for high performance by default, to the exclusion of low-end hardware. Very few sites that run FreeBSD servers do so without tuning the system for higher performance.

Performance tuning involves several different areas of the system, some of which require kernel reconfiguration (as you saw in Chapter 16). The following sections look at how to tune the kernel as well as components such as the disk.

### Kernel Settings

You will need to tune your kernel to support high levels of traffic if your machine will be handling extreme loads. The GENERIC kernel is tuned for workstation or low-load server use so that its hardware requirements can be as low as possible. High demand for kernel resources can overload a system that hasn't been optimized to support it.
