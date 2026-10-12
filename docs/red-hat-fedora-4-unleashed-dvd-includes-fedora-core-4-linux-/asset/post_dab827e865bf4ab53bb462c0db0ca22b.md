
In this situation, you should consider a virus scanner for your machine. You have several to choose from, both free and commercial. The most popular free suite is Clam AV (www.clamav.net), but Central Command, BitDefender, F-Secure, Kaspersky, McAfee, and others all compete to provide commercial solutions—look around for the best deal before you commit.

## Configuring Your Firewall

Always use a hardware-based or software-based firewall on computers connected to the Internet. Fedora includes a graphical firewall configuration client named `system-config-securitylevel`, along with a console-based firewall client named `lokkit`. Use these tools to implement selective or restrictive policies regarding access to your computer or LAN.

Start the `lokkit` command from a console or terminal window. You must run this command as root; otherwise, you will see an error message like this:

```
$ /usr/sbin/lokkit
ERROR - You must be root to run lokkit.
```

Use the `su` command to run `lokkit` like this:

```
$ su -c "/usr/sbin/lokkit"
```

After you press Enter, you see a dialog as shown in Figure 33.1. Press the Tab key to navigate to enable or disable firewalling. You can also customize your firewall settings to allow specific protocols access through a port and to designate an Ethernet interface for fire-walling if multiple NICs are installed. Note that you can also use a graphical interface version of `lokkit` by running the `gnome-lokkit` client during an X session.

![](img/774d40fd20903495c5cd00e2efad3f33_932_0.png)

**FIGURE 33.1** Fedora's `lokkit` command quickly generates firewall rules in memory for Linux.

Using `system-config-securitylevel` is a fast and easy way to implement a simple packet-filtering ruleset with filtering rules used to accept or reject TCP and UDP packets flowing through your host's Ethernet or designated device, such as `eth0` or `ppp0`. The rules are created on-the-fly and implemented immediately in memory using `iptables`.

Start `system-config-securitylevel` from the System Settings menu's Security level menu item. You are prompted for the root password and the client's window then appears. Figure 33.2 shows firewalling enabled for the eth0 Ethernet device, allowing incoming secure shell and HTTP requests.

![](img/774d40fd20903495c5cd00e2efad3f33_933_0.png)

**FIGURE 33.2** Fedora's `system-config-securitylevel` client can also be used to quickly generate and implement standard or simple custom firewall rules for Linux.

### Fedora and Firewalling

Fedora also supports the older—but still popular—ipchains packet-filtering software, which can be used to construct effective firewalling rules on Linux firewalls, gateways, servers, and workstations. Linux also supports the more capable iptables, or NetFilter system, which offers additional controls and logging facilities used to build filtering *rule sets* or filtering instructions.

Unfortunately, Fedora does not include any command-line or graphical interface utilities you can use to build, save, and test complex iptables rulesets, usually implemented as shell scripts. You need to do this if you want to control outgoing as well as incoming packets. However, you can write your own using a text editor such as vi. Many experienced Linux users hand-tune rulesets for specific application in advanced network situations, such as development of routing rules.

For a good overview and all the details about using iptables for a variety of gateway and firewall systems, read Robert L. Ziegler's excellent book, *Linux Firewalls, Second Edition*, available from New Riders. You can also browse to his site at http://www.linux-firewall-tools.com/linux/firewall/index.html, which offers a graphical, web-based firewall design and construction tool you can use to quickly build a custom ipchains-based ruleset file.

You can use Fedora to create a custom firewall, perhaps supporting IP masquerading (also known as *NAT*) by using either ipchains or iptables. You'll find two sample scripts under the /usr/share/doc/rp-pppoe/configs directory; these are used when connecting to the Internet using a digital subscriber line (DSL).

## Forming a Disaster Recovery Plan

No one likes planning for the worst, which is why two thirds of people do not have wills. It is a scary thing to have your systems hacked: One or more criminals has broken through your carefully laid blocks and caused untold damage to the machine. Your boss, if you have one, will want a full report of what happened and why, and your users will want their email when they sit down at their desks in the morning. What to do?

If you ever do get hacked, nothing will take the stress away entirely. However, if you take the time to prepare a proper response in advance, you should at least avoid premature aging. Here are some tips to get you started:

-   Do not just pull the network cable out—This alerts the hacker that he has been detected, which rules out any opportunities for security experts to monitor for that hacker returning and actually catch him.
-   Only inform the people who need to know—Your boss and other IT people are at the top of the list; other employees are not. Keep in mind that it could be one of the employees behind the attack, and this tips them off.
-   If the machine is not required and you do not want to trace the attack, you can safely remove it from the network—However, do not switch it off because some backdoors are only enabled when the system is rebooted.
-   Take a copy of all the log files on the system and store them somewhere else—These might have been tampered with, but they might contain nuggets of information.
-   Check the `/etc/passwd` file and look for users you do not recognize—Change all the passwords on the system, and remove bad users.
-   Check the output of `ps aux` for unusual programs running—Also check to see whether any cron jobs are set to run.
-   Look in `/var/www` and see whether any web pages are there that should not be.
-   Check the contents of the `.bash_history` files in the home directories of your users—Are there any recent commands for the root user?
-   If you have worked with external security companies previously, call them in for a fresh audit—Hand over all the logs you have, and explain the situation. They will be able to extract all the information from the logs that is possible.
-   Start collating backup tapes from previous weeks and months—Your system might have been hacked long before you noticed, so you might need to roll back the system more than once to find out when the attack actually succeeded.
-   Download and install Rootkit Hunter from `http://www.rootkit.nl/projects/rootkit_hunter.html`—This searches for (and removes) the types of files that bad guys leave behind for their return.

Keep your disaster recovery plan somewhere safe; saving it as a file on the machine in question is a very bad move!

## Keeping Up-to-Date on Linux Security Issues

A multitude of websites relate to security. One in particular hosts an excellent mailing list. The site is called Security Focus, and the mailing list is called BugTraQ. BugTraQ is well-known for its unbiased discussion of security flaws. Be warned: It receives a relatively large amount of traffic (20–100+ messages daily).

Often security holes are discussed on BugTraQ before the software makers have even released the fix. The Security Focus site has other mailing lists and sections dedicated to Linux in general and is an excellent resource.

## Related Fedora and Linux Commands

You will use these commands when managing security in your Fedora system:

-   `Ethereal`—GNOME graphical network scanner
-   `gnome-lokkit`—Fedora’s basic graphical firewalling tool for X
-   `lokkit`—Fedora’s basic graphical firewalling tool
-   `ssh`—The OpenSSH remote login client and preferred replacement for `telnet`
-   `system-config-securitylevel`—Fedora’s graphical firewall configuration utility

## Reference

-   http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/s1-basic-firewall-gnomelokkit.html—Red Hat’s guide to basic firewall configuration. Newer documentation will appear at http://fedora.redhat.com.
-   http://www.insecure.org/nmap/—This site contains information on Nmap.
-   http://www.securityfocus.com/—The Security Focus website.
-   http://www.tripwire.org—Information and download links for the open-source version of Tripwire.
