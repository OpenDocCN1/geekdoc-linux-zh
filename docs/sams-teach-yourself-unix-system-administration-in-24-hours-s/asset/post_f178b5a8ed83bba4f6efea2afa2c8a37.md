
if the cracker has broken into one system, he's therefore broken into the entire trusted set). Disable rlogin by removing the rlogin and rshd binaries.

## Unnecessary Network Services

This leads to a general observation: Shut off all services that are unnecessary to the day-to-day use of your system. You probably don't need to run the rwho daemon, for example, or talkd or fingerd. Shut them off in xinetd or an equivalent—(see Hour 19 for details).

Speaking of unnecessary network services, turn off telnet and ftpd now. If your users need to log in to the system, instruct them to use ssh and point them to some ssh-compliant client programs (check at www.download.com). The ssh system also supports secure file transfers, and there are ssh-compliant FTP clients available online, too.

When you're done turning things off, run the useful nmap utility to scan your ports and inform you what's still running:

```
# nmap -sT localhost
Starting nmap V. 2.54BETA22 (www.insecure.org/nmap/)
Interesting ports on localhost.localdomain (127.0.0.1):
(The 1536 ports scanned but not shown below are in state: closed)
Port     State    Service
22/tcp   open     ssh
25/tcp   open     smtp
111/tcp  open     sunrpc
1024/tcp open     kdm
1025/tcp open     listen
6000/tcp open     X11

Nmap run completed -- 1 IP address (1 host up) scanned in 3 seconds
```

Here you can see that it might be smart to disable kdm (the KDE desktop manager), sunRPC (the SunOS remote procedure call mechanism), and X11 (the X Window System server).

## Keep Your Operating System Up-To-Date

One of the most important security measures you can take as a system administrator is to ensure that your Unix operating system is always up-to-date. It's common for sysadmins to run old operating systems that have all sorts of known—and fixed—security problems, and that's clearly a bad idea.

Regardless of which Unix you have, your vendor's Web site should have any patches and updates, and most have e-mail lists you can join that notify you proactively of any security holes and how to fix them. Pay attention to this!

## Join the Computer Emergency Response Team

One U.S. government-funded group that does a great job of keeping an eye on security problems and promptly issuing warnings and notifications across a wide variety of different operating systems is CERT, the Computer Emergency Response Team at Carnegie-Mellon University. You can find it online at www.cert.org, then sign up for their mailing list.

## Other Useful Web Sites

There are a couple of other sites worth exploring if you want to learn more about securing your Unix systems: The Computer Incident Advisory Capability (www.ciac.org), Rootshell (www.rootshell.org), Security Focus (www.securityfocus.com), and the System Administration, Networking and Security group (www.sans.org) are all well worth spending time exploring.

## Useful Tools

There are a number of third-party security tools available that help you batten down the hatches and keep an electronic eye on what's happening. Chief among them are swatch, an elegant and simple system logfile watchdog; tripwire, a tool that snapshots all the system binaries and informs you of any change (for example, a cracker trying to sneak a Trojan horse onto the system); crack, an effective password guesser that lets you enforce a "non-guessable" password policy; and ipchains, a firewall that's included with many modern flavors of Unix. Other tools worth exploring if you want to really ratchet up your protection include COPS, SATAN, SAINT, tcpd, and TCT.

Start your search for these sophisticated security tools at an appropriate package management archive Web site (see Hour 8, "Unix Package Management"), or search at the USENIX System Administration Guild (SAGE) Web site (www.usenix.org/sage/) for details.

## Summary

The most important security strategy is to be paranoid, circumspect, suspicious, secretive, and open and friendly at the same time. Seriously, be conscious of security and security issues, teach your user community simple steps—like picking good passwords—and do your best to create an open and productive work environment, while still doing regular backups, rotating your backup media to ensure you always have at least one "spare" backup image.

## And So Our 24 Hours Come to an End...

This marks the end of the 24th hour of Teach Yourself Unix System Administration in 24 Hours. It's been quite a journey, and there's been a remarkable amount of material covered, much of which takes some time to digest and understand properly. So, whether you've slammed through in 24 hours, or whether you've taken a few weeks to slowly step through and understand each topic, it's time to use what you've learned in this book. It's only through use that you'll truly learn how to think and work like a top Unix system administrator, comfortable in front of a command line and able to convince your systems to jump through hoops of your own making.

Good luck!

Remember, if you encounter any errata in this book, any examples that you cannot duplicate, typographical mistakes, or other problems, please let us know! Go to www.intuitive.com/tyusa/ and you'll find an errata report form there.

And stay in touch.

Dave Taylor

taylor@intuitive.com

![](img/5ced0c78d748bd190e9027e5549a3622_499_0.png)

## INDEX

### A

- Acceptable Use Policy (AUP), 402
- access
  - accounts, 108
  - CERT, 481
  - crontab, 286-291
  - /etc/passwd file, 86-90
  - groups
    - /etc/group, 73-76
    - security, 77-79
  - hackers, 307-311
  - inetd, 379-381
  - passwords, 91-94, 479
  - Red Hat Linux, 14
  - rlogin, 479
  - strings, 67
    - /etc/passwd, 70-73
    - files, 68-70
  - unnecessary network services, 480
  - updating, 480
  - Web sites, 481
- access.log file, 316
- accounts
  - Darwin password files, 91-94
  - deleting, 112-114
  - Linux management tools, 114-121
  - passwords, 126-129
  - re-enabling, 111
  - Red Hat Linux, 14
  - Solaris management tools, 121-126
  - suspending, 108-111
  - user, 89
- actions, init, 250
- adding
  - drives, 208-212
  - users, 94-103
- addresses
  - IP, 333
  - ranges, 328
- adduser command, 98, 100-103
- adduser script, 94-95
- administration
  - accounts
    - deleting, 112-114
    - suspending, 108-111
  - databases, 354-358
  - inetd, 379-381
  - files
    - sizing, 134-138
    - zipping, 138-142, 144-148
  - packages
    - Darwin, 168-172
    - Solaris, 172-176
  - log files, 301-302
    - building rotation tools, 320-323
    - httpd, 312-316
    - navigating, 302-307
    - tracking hackers, 307-311
    - trimming with logrotate, 317-320
  - passwords, 126-129
  - processes, 276-279
  - RPM, 162-165
  - scripts, 59-63
  - tools
    - artsd, 273-275
    - at command, 296-298
    - compress, 134-138
    - crontab, 286-291
    - dig, 364-370
    - du command, 47-52
    - fsck, 182-193
    - gzip, 138-142, 144
    - host, 364-370
    - ifconfig, 343-349
    - management, 114-121, 121-126
    - netstat, 343-349
    - passwords, 126-129
    - ping, 343-349
    - popd, 463
    - pushd, 463
    - rotation, 320-323
    - virtual hosts, 474-478
    - xinetd, 381-385
- aging passwords, 126-129
- aliases, creating, 404-411
- alphabetization, sort tool, 53-55
- anacron daemon, 287, 435
- anonymous FTP service, 386. See also FTP
- Apache Web server
  - http log files, 312-316
  - httpd.conf file, 462-467
  - optimizing, 467-471
  - starting, 458-461
  - virtual hosting, 474-478
- applications
  - artsd, 273-275
  - at command, 296-298
  - compress, 134-138
  - crontab, 286-291
  - dig, 364-370
  - du command, 47-52
  - fsck, 182
    - applying, 186-189
    - single-user mode, 190-193
    - starting, 183-186
  - gzip, 138-142, 144
  - host, 364-370
  - ifconfig, 343-349
  - management
    - Linux, 114-121
    - Solaris, 121-126
  - named, 359-362
  - netstat, 343-349
  - passwords, 126-129
  - ping, 343-349
  - popd, 463
  - pushd, 463
  - rndc, 362-364
  - rotation, 320-323
  - sort, 52-55
  - tar, 148-158
  - tools
    - artsd, 273-275
    - at command, 296-298
    - compress, 134-138
    - crontab, 286-291
    - dig, 364-370
    - du command, 47-52
    - fsck, 182-193
    - gzip, 138-142, 144
    - host, 364-370
    - ifconfig, 343-349
    - management, 114-121, 121-126
    - netstat, 343-349
    - passwords, 126-129
    - ping, 343-349
    - popd, 463
    - pushd, 463
    - rotation, 320-323
    - virtual hosts, 474-478
    - zip, 145-148
- applying
  - Apache Web servers, 464
  - DNS, 364-370
  - dual-booting, 218-219
  - GRUB, 223-226
  - LILO, 220-223
  - partitioning disks, 219-220
  - virtual machines, 226-228
  - fink, 172
  - fsck tool, 186-189
  - init processes, 248, 250-253
  - installation, 8-10
  - logrotate, 317-320
  - Mac OS X, 336-343
  - named application, 359-362
  - networks, 327
    - connecting Linux to Internet, 328-335
    - Mac OS X/Solaris, 336-343
    - testing, 343-349
  - passwords, 95-99
  - Red Hat Linux
    - keyboards, 10
    - network connections, 13
  - rndc application, 362-364
  - RPM, 162-167
  - reloading, 362
  - run levels, 254-259
  - shell scripting, 436, 438-440
  - Solaris, 336-343
  - tools
    - artsd, 273-275
    - at command, 296-298
    - compress, 134-138
    - crontab, 286-291
    - dig, 364-370
    - du command, 47-52
    - fsck, 182-193
    - gzip, 138-142, 144
    - host, 364-370
    - ifconfig, 343-349
    - management, 114-121, 121-126
    - netstat, 343-349
    - passwords, 126-129
    - ping, 343-349
    - popd, 463
    - pushd, 463
    - rotation, 320-323
    - virtual hosts, 474-478
