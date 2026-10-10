
Startup problems can be particularly troublesome because they leave you with a nonfunctional FreeBSD system, or at best, one that works suboptimally. In many cases, using an emergency startup system, as described in the upcoming section, “Using an Emergency Boot System,” can help you correct the problem by providing a minimally functional FreeBSD system. In a few cases, using another OS can also help; for instance, you might be able to install another OS’s boot loader to replace a damaged or misbehaving FreeBSD Stage 0 boot loader.

## Device Driver Problems

Some device driver problems prevent the computer from booting. For instance, if a system with a SCSI hard disk and no IDE disk lacks drivers for the computer’s SCSI host adapter, FreeBSD won’t be able to boot. It may get partway through the kernel boot messages, but it will fail before being able to run any boot scripts. Such problems are likely to manifest themselves at system installation or when using a newly compiled kernel for the first time.

Less extreme driver problems produce more subtle symptoms—but “more subtle” in this context includes some pretty nasty happenings, such as random system crashes. Other problems include an inability to use devices that aren’t critical for the system to boot, such as a sound card or Ethernet interface; odd errors when using such devices, such as distortion when playing sound files; and poor performance, such as sluggish disk accesses. In sum, driver problems produce symptoms that are very similar to those produced by defective hardware.

Much of the task of diagnosing driver problems relates to isolating the problem as being hardware or software. You can use techniques such as hardware swapping between computers and tests in multiple OSes to help make this diagnosis—but remember that these tests can sometimes lead you astray. For instance, two OSes might have similar bugs in their device drivers, particularly if the OSes are closely related; and it’s always possible you’ll have two defective boards.

Fixing device driver problems requires upgrading the kernel to a version that includes fixed drivers, or recompiling a kernel so that it includes a driver that was originally omitted. In a few cases, using `kldload` to load a driver module is all that’s required. Chapter 12 describes all these topics.

## Networking Software Problems

Networking problems can be difficult to track down because the networking subsystem is quite complex. Some networking problems are related to network hardware or drivers, but many problems are related to software or configuration. Common problem areas include:

- **Network hardware and drivers** Network hardware can be defective, and network drivers can be buggy. If your network connection seems to be flaky overall, you should investigate these issues.

- **Network startup scripts** The `/etc/network` startup script controls the network startup process. This script relies upon settings in other scripts, most notably `/etc/rc.conf`. The basic network interface configuration is defined here, as is the startup of many network servers. Chapter 14 and other chapters of Part III describe these issues in detail. Typos or more severe misconfiguration can cause problems ranging from a complete inability to use the network to subtle errors on the part of servers.

- **Server configuration files** Most servers use their own configuration files to set server-specific options. If a single server isn't functioning as you expect, these files are a good place to start looking for answers, in conjunction with appropriate documentation and log files. Configuration errors can produce a wide range of symptoms, ranging from a complete lack of response by the server to subtle misbehaviors.

- **Firewalls** If you configure a firewall, as described in Chapter 17, that firewall might interfere with the normal functioning of both clients and servers. The typical symptom is a complete inability to contact outside systems using a client, or of a server to respond to requests sent from outside systems. Even a firewall that's not located on your own computer can cause problems; routers sometimes include firewalls that block access to particular ports for security reasons. Consult whoever operates your local router if you suspect this to be the case.

- **DNS problems** The Internet relies heavily upon the Domain Name System (DNS) to convert hostnames into IP addresses and vice-versa. One common network configuration problem is a mis-setting of the DNS computer. The `/etc/resolv.conf` file sets from one to three DNS computers, specified by IP address on `nameserver` lines. If these computers' IP addresses are set incorrectly, or if the DNS servers have crashed, you won't be able to access remote computers by name, but IP addresses will still work.

- **Program-specific bugs** Both clients and servers can suffer from bugs. These bugs produce program-specific symptoms ranging from program crashes to subtle quirks. The usual solution is to upgrade the program to a fixed version.

One key to network diagnostics is to try to reproduce the problem on multiple computers. For instance, if you can't reach particular outside web sites on any computer on your network, chances are good that the problem is on the external computers, in firewall blocks, or with similar issues, rather than problems on the web browser systems. If the problems occur only on some systems, look for commonalities. For instance, perhaps all the problem systems are running a particular version of the web browser, or they're all on a single subnet. These commonalities can be important clues to the cause of the problem.

## User Program Problems

Programs run by ordinary users can be buggy. Unfortunately, the range of possible bugs in such programs is extremely wide. Fortunately, it's usually fairly obvious that the problem is isolated to just one program because it's the only one that exhibits any odd behavior. Bug libraries can cause problems in many programs, though.

As a general rule, a good place to begin when investigating reports of problems from users is to attempt to reproduce the problem in a new account. Some problems are caused by errors in the user's own configuration files. In such a case, testing the software in a new account may turn up no problems, which narrows the range of possible causes to configuration issues, including the user's own configuration files and issues such as permissions on the user's / or common files or directories and configuration problems related to the user's group. You can use `diff` to compare the user's configuration files to those in a fresh account and investigate possible configuration issues.

If you run into the same problems in a new account that an existing user reports, you may want to investigate the software itself. It may be buggy or have a misconfiguration in a global configuration file. Bug fixes for user programs are not uncommon, so you may want to look for an updated version of the software.

Some problems with user programs are related to permissions. For instance, audio software needs access to the sound card devices. A default FreeBSD installation enables ordinary users to write to the sound card device files, as described in Chapter 27, but you may have changed this configuration. Such access might not exist for all software; for instance, tape backup and CD-R packages require access to the tape and CD-R devices, respectively, but normally only root may access these devices. You may need to change this configuration if ordinary users should be able to use these devices.

It's possible that you're the first person to encounter a bug. If your bug seems fairly exotic—say, if it happens only under a very particular and odd set of circumstances—you may need to contact the program's official web page for details. Sometimes you may submit a bug report via e-mail. Other times (particularly for large projects) you may need to use a web-based bug report system. If you know enough about the programming language and relevant toolkits used by the program, you can try debugging it yourself and then submitting the fix to the author. In fact, this can be an excellent way to give back to the open source community that created FreeBSD.

## Testing a Solution

In many cases, identifying a problem and solving the problem go hand in hand; diagnostic techniques involve making changes that, if successful in identifying the problem, also solve the problem. Once you've solved a problem, though, you may want to further test the affected subsystem. For instance, if a program has been crashing frequently and you've upgraded the program to a version that seems more stable, you may want to test the program more extensively—say, by running it for a long period of
