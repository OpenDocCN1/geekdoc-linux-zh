
## 7.11.2 Starting the Firewall on Boot with Red Hat and SUSE

On Red Hat and SUSE, the simplest way to initialize the firewall is to edit `/etc/rc.d/rc.local` and add the following line to the end of the file:

```
/etc/rc.d/rc.firewall start
```

After the firewall rules are debugged and stable, Red Hat Linux provides a more standard way to start and stop the firewall. If you choose iptables while using one of the run-level managers, the default runlevel directory contains a link to `/etc/rc.d/init.iptables`. With the other startup scripts in this directory, the system will start and stop the firewall automatically when booting or changing runlevels.

One additional step is required to use the standard runlevel system, however. You must manually install the firewall rules:

```
/etc/rc.d/rc.firewall
```

Then execute the command:

```
/etc/init.d/iptables save
```

The rules will be saved in a file, `/etc/sysconfig/iptables`. After this, the startup script will find this file and load the saved rules automatically.

A word of caution is in order about saving and loading the firewall rules using this method. The iptables save and load features are not fully debugged at this point. If your particular firewall configuration results in a syntax error when saving or loading the rules, you must continue using some other startup mechanism, such as executing the firewall script from `/etc/rc.d/rc.local`.

## 7.11.3 Starting the Firewall on Boot with Debian

As with many other things, configuring the firewall script to start on boot is simpler on Debian than other distributions. You can make the firewall start and stop on boot with the `update-rc.d` command. Run `update-rc.d` with the firewall script in `/etc/init.d`, and set your current directory to `/etc/init.d/` as well:

```
cd /etc/init.d
update-rc.d rc.firewall defaults
```

See the man page for `update-rc.d` for more information on its usage beyond that shown here.

Other aspects of the firewall script depend on whether you have a registered, static IP address or a dynamic, DHCP assigned IP address. The firewall script as presented in this chapter is set up for a site with a statically assigned, permanent IP address.

## 7.11.4 Installing a Firewall with a Dynamic IP Address

If you have a dynamically assigned IP address, the standard firewall installation method will work without modification. The firewall rules would be installed before the network interfaces are brought up, before the system is assigned an IP address, and possibly before being assigned a default gateway router or name servers.

The firewall script itself needs the IPADDR and NAMESERVER values defined. Both the DHCP server and the local `/etc/resolv.conf` file can define up to three name servers. Also, given any site may or may not know the addresses of their DNS servers, default gateway router, or DHCP server ahead of time. Furthermore, it's not uncommon for your network mask, subnet, and broadcast addresses to change over time as the ISP updates its network. Some ISPs assign a different IP address on a frequent basis, with the result that your IP address can change numerous times during the course of an ongoing connection.

Your site may provide some means of dynamically updating the installed firewall rules as these changes.

In addition, if you are using a DSL connection, there's a chance the MTU might cause problems. If this is the case, here's a firewall rule to fix the problem:

```
$IPT -A OUTPUT -o $INTERFACE -p tcp --tcp-flags SYN, RST \ \
SYN -j TCPMSS --clamp-mss-to-pmtu
```

The firewall script could read these shell variables directly from the environment or could read them from a file. In any case, the variables would not be hard-coded into the firewall script, as they are in the example in this chapter.

## 7.12 Summary

This chapter led you through the processes involved in developing a standalone firewall using iptables. The deny-by-default policy was established. Some commonly used attack vectors were fixed at the beginning of the script, including source address spoofing, protecting services running on privileged ports, DNS. Examples of popular network services were shown. ICMP, the control and status messages used by the underlying IP Network layer, were handled as well. Examples of controlling the level of logging were demonstrated. Finally, the issues involved in firewall installation were described, both for sites with a static IP address and for sites with a dynamically assigned IP address.

# PART II

## DETECTING AN INTRUSION

This whole book is about reducing the probability, severity, and consequences of intrusions. Be realistic. No system is 100 percent secure and anyone who claims that his system or his products are 100 percent secure is a fool or a liar. 99 percent of the people reading this book will have someone attempt to break into their systems. Without changing your configuration, you can reduce the risk by monitoring activity.

Perhaps 10–20 percent of people reading this book will suffer a system break-in. Those who are scared by this statistic and are considering another book or switching to another operating system instead are encouraged to reread the previous paragraph!

The suggestions in Part I were a methodical approach to eliminating known security holes in the varying parts of your system and network. Now comes the vigilant watch for intrusion attempts. If following the advice of the previous parts of this book makes your system so secure, why should you care about thwarted attacks? As I write, the current versions of all Linux distributions have a known DNS vulnerability, due to a bug in the new version of the `named` program. By monitoring system and network activity, you may detect these intrusions quickly and eliminate the consequences.

It is important to monitor the security sites discussed in Appendix C so you can update your system when someone gets broken into, before the same exploit happens to open your systems. However, this is not a cure-all. One of my clients suffered a break-in in late 1999, via FTP, a method that had not been discussed in the security sites (which I had been monitoring very closely while conducting research for this book).

The log files indicated suspicious FTP activity with time-stamps indicating it happened shortly before the cracker installed some files. The logs indicated no email or DNS activity. This was enough to satisfy me as the means of the attack. Certainly, an extremely sophisticated cracker had planted false logs, but this is very unusual and this incident looked like the work of a script kiddie. Even a post-mortem search of the security sites turned up only a brief mention that it had happened to someone else, with no clues as to the vulnerability more specific than “FTP”

I concurred with the MIS Department that TCP Wrappers would prevent a re-occurrence and TCP Wrappers were installed. No subsequent problems were encountered. If automatic logging to another system is set up, you might have clues as to how the penetration was done, even if a sophisticated cracker has cleaned your log files of incriminating evidence. This will allow you to know where to harden your system to avoid a repeat attack from the same cracker or a different one.

Do not discount the value of log files in convincing management of the importance of budgeting for security work. The log files will help prevent a break-in. Log files help put crackers out of business. Personally, I have caused a number of cracker accounts to be shut down by providing a detailed report of their attempts against my systems to their ISPs, explaining how “trying to connect to known cracker ports, Sun RPC ports, and the like could not possibly be considered legitimate access.” In one case I caused an account owner to be informed that his account has been compromised (well, at least that is what he told his ISP). This has happened often enough that I have been tempted to modify the blockkip Adaptive TCP Wrappers program to generate this e-mail automatically; it certainly would be easy enough.

> ¹ My server does not provide RPC services, telnet, ftp, or other services. By monitoring these ports, I know when attacks are directed to these ports and my systems lock these crackers out automatically. This might be considered as acting as a honeypot; that is, providing something sweet to attract crackers away from something more valuable or sensitive.
