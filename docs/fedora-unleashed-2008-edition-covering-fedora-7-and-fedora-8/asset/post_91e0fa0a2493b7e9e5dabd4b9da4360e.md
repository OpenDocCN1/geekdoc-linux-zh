
**FIGURE 30.2** Fedora's system-config-securitylevel client can also be used to quickly generate and implement standard or simple custom firewall rules for Linux.

You can use Fedora to create a custom firewall, perhaps supporting IP masquerading (also known as NAT) by using either ipchains or iptables. You'll find two sample scripts under the /usr/share/doc/rp-pppoe/configs directory; these are used when a digital subscriber line (DSL) is used for Internet connection.

# Forming a Disaster Recovery Plan

No one likes planning for the worst, which is why two-thirds of the population do not have a will. It is a scary thing to have your systems hacked: One or more criminals have broken through your carefully laid blocks and caused untold damage to the machine. Your boss, if you have one, will want a full report of what happened and why, and your users will want their email when they sit down at their desks in the morning. What to do?

If you ever do get hacked, nothing will take the stress away entirely. However, if you take the time to prepare a proper response in advance, you should at least avoid premature aging. Here are some tips to get you started:

- **Do not just pull the network cable out**—This alerts the hacker that he has been detected, which rules out any opportunities for security experts to monitor for that hacker returning and actually catch him.
- **Inform only the people that need to know**—Your boss and other IT people are at the top of the list; other employees are not. Keep in mind that it could be one of the employees behind the attack, and this tips them off.
- **If the machine is not required and you do not want to trace the attack, you can safely remove it from the network**—However, do not switch it off because some backdoors are enabled only when the system is rebooted.
- Make a copy of all the log files on the system and store them somewhere else—These might have been tampered with, but they might contain nuggets of information.
- Check the /etc/passwd file and look for users you do not recognize—Change all the passwords on the system, and remove bad users.
- Check the output of `ps aux` for unusual programs running—Also check to see whether any cron jobs are set to run.
- Look in `/var/www` and see whether any web pages are there that should not be. If you see any you don’t recognize, check them closely and move them into a quarantined area if need be.
- Check the contents of the `.bash_history` files in the home directories of your users—are there any recent commands for the root user?
- If you have worked with external security companies previously, call them in for a fresh audit—Hand over all the logs you have, and explain the situation. They will be able to extract all the information from the logs that is possible.
- Start collating backup tapes from previous weeks and months—Your system might have been hacked long before you noticed, so you might need to roll back the system more than once to find out when the attack actually succeeded.
- Download and install Rootkit Hunter from http://www.rootkit.nl/projects/rootkit_hunter.html—This searches for (and removes) the types of files that bad guys leave behind for their return.

Keep your disaster recovery plan somewhere safe; saving it as a file on the machine in question is a very bad move!

# Keeping Up-to-Date on Linux Security Issues

A multitude of websites relate to security. One in particular hosts an excellent mailing list. The site is called Security Focus, and the mailing list is called BugTraQ. BugTraQ is well-known for its unbiased discussion of security flaws. Be warned: It receives a relatively large amount of traffic (20–100+ messages daily). The archive is online at http://www.securityfocus.com/archive/1.

Security holes are often discussed on BugTraQ before the software makers have even released the fix. The Security Focus site has other mailing lists and sections dedicated to Linux in general and is an excellent resource.

# Understanding SELinux

Users moving from Windows to Linux often make the mistake of wanting to maximize the security of their system by changing the default Linux settings "to what they ought to be." If that's you, stop right there: Fedora is designed to be secure out of the box, which means you need to change nothing to be secure.

One of the most commonly misunderstood components of the Fedora security ecosystem is SELinux, which was designed by the US government's National Security Agency to ensure that Linux meets its high requirements for technology security. What people misunderstand about SELinux is that it works automatically, out of the box, whether you understand it or not; you don't need to enable it, tweak it, or even know how it works for it to help keep your system secure. SELinux is designed to complement, rather than replace, the existing Linux security permissions system, which means that anything allowed by SELinux but disallowed by your file system permissions is denied.

SELinux works by monitoring every system request of every program. For example, each time Apache wants to serve a web page, it has to ask SELinux whether it can read the requested file. Don't worry, the speed hit is minimal; but in terms of security, it means that even if Apache is compromised, it still can't be used to read sensitive files because SELinux stops it.

The only time you are likely to run into SELinux is when a program tries to do something it shouldn't. This might mean you have a security problem, but might also mean your system is trying to do something that the Fedora developers hadn't anticipated. Either way, you'll see a small bubble appear in the top-right corner of your screen, saying AVC denial, click icon to view. When you click the icon, the SELinux troubleshoooter app appears, explaining what happened and why it was blocked. The troubleshoooter also tells you what to do if the request was legitimate and you want to allow it in the future.

One last word of advice: even if SELinux does get in your way now and then, don't disable it. Several previous Linux security vulnerabilities have been exploited on other distros, but stopped on Fedora thanks to SELinux, which proves it works. Having your file system permissions set correctly, keeping SELinux enabled, and using the built-in firewall all helps to keep your system secure—make the most of it!

# Related Fedora and Linux Commands

These commands are used to manage security in your Fedora system:

- **Ethereal**—GNOME graphical network scanner
- **gnome-lokkit**—Fedora's basic graphical firewalling tool for X
- **lokkit**—Fedora's basic graphical firewalling tool
- **ssh**—The OpenSSH remote login client and preferred replacement for **telnet**
- **system-config-securitylevel**—Fedora's graphical firewall configuration utility

# Reference

- [http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/s1-basic-firewall-gnomelokkit.html](http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/s1-basic-firewall-gnomelokkit.html)—Red Hat's guide to basic firewall configuration. Newer documentation will appear at [http://fedora.redhat.com/](http://fedora.redhat.com/).
- [http://www.insecure.org/nmap/](http://www.insecure.org/nmap/)—This site contains information on Nmap.
- [http://www.securityfocus.com/](http://www.securityfocus.com/)—The Security Focus website.
- [http://www.tripwire.org/](http://www.tripwire.org/)—Information and download links for the open-source version of Tripwire.

# CHAPTER 31

# Performance Tuning

IN THIS CHAPTER
- Hard Disk
- Kernel
- Apache
- MySQL
- Reference

Squeezing extra performance out of your hardware might sound like a pointless task given how cheap commodity upgrades are today. To a certain degree that is true—for most of us, it is cheaper to buy a new computer than to spend hours fighting to get a 5% speed boost. But what if the speed boost were 20%? How about if it were 50%?

The benefit you can get by optimizing your system varies depending on what kinds of tasks you are running, but there is something for everyone. Over the next few pages, we look at quick ways to optimize the Apache web server, both the GNOME and KDE desktop systems, both MySQL and PostgreSQL database servers, and more.

Before you start, you need to understand that optimization is not an absolute term: If you optimize a system, you improve its performance, but it is still possible it could further be increased. Getting 99.999% performance out of a system is not the objective because optimization suffers from the law of diminishing returns—the basic changes make the biggest differences, but after that it takes increasing amounts of work to obtain decreasing speed improvements.

# Hard Disk

Many Linux users love to tinker under the hood to increase the performance of their computers, and Linux gives you some great tools to do just that. Whereas others tell us, "Don't fix what's not broken," fathers often say, "Fix it until it breaks." In this section, you learn about many of the commands used to tune, or "tweak," your file system.

Before you undertake any "under the hood" work with Linux, however, keep a few points in mind. First, perform a benchmark on your system before you begin. Linux does
