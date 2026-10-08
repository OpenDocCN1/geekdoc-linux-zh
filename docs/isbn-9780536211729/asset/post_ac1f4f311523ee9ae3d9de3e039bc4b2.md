
Sometimes you no longer remember the password needed to log in to a system. Sometimes the system will not boot up so it is considered “safe” for disposal, but the boot problem might not be due to a defective disk. In this case a “bad guy” or even a “gray hat” could remove the disk, connect it to another system, and possibly read the data.

All disks should be erased or destroyed prior to disposal. The new owner of the system can install Linux herself if she desires. Most competing closed source software is sold via a nontransferable license, so one cannot legally leave it on the disk anyway. This means that you are obligated legally to erase the closed source from the disk.

## A.12 Network Topology Policy

![](img/7d04225c75a86d3cf4bd6077596f35b2_560_0.png)

By *topology*, I mean network configuration or how the different parts of your network are connected (shaped). The topology or shape of networks can differ greatly, and has a huge effect on the security as well as the performance of the network and should be thought out carefully. Most networks start out small and grow haphazardly. Certainly, planned growth is preferred. When this is not possible, please do consider analyzing and reorganizing the topology periodically, perhaps annually.

- The topology policy should forbid anyone other than the SysAdmins (or possibly the Network Admins) from altering the network. This especially means forbidding desktop users from putting modems on their networked systems and connecting to the Internet (or any unsecured or untrusted system).

Laptops are a special problem, because most users need to dial up to get their e-mail on the road and want to hook into the organization’s Ethernet when at the office. If they get their e-mail only from the company system, prohibiting them from dialing into noncompany systems might be a good solution.

The reason for avoiding ISPs is that because the ISP does not know what services you want or from whom, you are wide open to attack. For a laptop whose user still needs to connect to an ISP, say to get e-mail from her home account, the solution is to secure it as if it were a corporate system outside a firewall, because it is. All incoming services should be blocked, especially telnetd, FTP, and SMTP (sendmail or its equivalent) and any program that handles incoming packets such as the FTP, telnet, and POP clients should be up-to-date versions of programs that have a good history of being secure.

The reason for this concern about systems that can access the Internet (without the protection of the firewall that you carefully set up) is that any decent cracker can easily break into almost any Windows or NT box from the dial-up connection. Then he will be in your corporate network, bypassing your carefully set-up firewall. A laptop running Linux too is vulnerable unless it is secured with the same thoroughness as the corporate Web server or mail server. This is discussed in “Stopping End Runs Around Firewalls” on page 68.

Policy should also forbid any other unauthorized (and unplanned) change to network topology, especially connections to the Internet or reorganizations of subnets that might join separate departments or bridge around intracompany firewalls.

- I was told that a manager at one office of a large Southern U.S. bank was unhappy with the speed of the corporate Internet connection, so he ordered his own T1 Internet connection for his branch without worrying about security, thus endangering the entire bank's data and money.

This same bank had automatic equipment regularly dial every phone number in the company to detect any numbers that had modems connected to them in violation of company policy. Every time they ran this check, they would find a surprising number of modems and then would send someone out to eliminate them.

### A.12.1 Internal Network Topology Policy

Many organizations, large and small, and even those with home networks, need to consider their internal network topology. Certainly, insecure systems need to be kept isolated from the Internet via firewalls but unfortunately this is the extent of security at most companies. It is important to ask “What if?” What if one of the managers, with his Windows laptop plugged into the network, dials into his home ISP with PPP to get e-mail and in this configuration a cracker comes in through the PPP connection and gains control of his Windows laptop?

This possibility exists for Linux laptops too. What if one of the engineers wanted to connect to her system from home but did not want to bother with SSH and insisted that the firewall let telnet into her work system? What if a cracker broke into that system? What if one of your employees felt maltreated by her boss (legitimately or not) and wanted to hurt the company? What if someone loaded some software from the Web that had a Trojan horse? What if your Web server was broken into?

Would your network topology then grant the rogue access to all of your systems? Most companies assume that the only point of intrusion is from the Internet and that a carefully configured firewall will solve all their problems. Unfortunately, this is a plan for disaster.

Draw a diagram of your network listing your systems (or one or two systems in each category), and apply these What if scenarios. How many systems could a cracker easily get to? How good are the passwords on critical systems? Consider that about half of all security incidents originate on an inside system and of the remaining half, once a cracker gets into one of your systems, frequently he will try to get into as many as possible and cause as much damage as possible. Put low security systems (such as Windows and other unsecured boxes and similar client systems) on a different network (or subnet) separated by a firewall from high security systems. Put different departments on separate networks with firewalls between them.

Low-security systems with highly confidential information should be on a separate network (possibly several different networks) that cannot be accessed from other networks and the Internet. These might include accounting systems that control payroll and accounts payable that definitely should be on a network isolated from everything else in the company and really, really should not have any Internet access. These systems should be configured so that non-SysAdmins are unable to install software to prevent viruses and Trojans or even general-purpose network software such as Netscape from being loaded. Unless needed to do their jobs, these systems should not have floppy or CD-ROM drives and any general-purpose software for importing software should be removed so that “you can’t get here from there.”

If they must have a floppy or CD-ROM drive to import data or some way to import data over the network, get or create a special-purpose program or script to do this in a controlled manner. Please give these people a separate machine with Netscape and e-mail so that they will be less tempted to subvert the very important security walls you have set up.

Your engineering systems should be on a separate network from the rest of the company, because engineers are frequently experimenting, and the experimental systems have not been hardened for security. You probably want “lab” systems that frequently are changing (and therefore are least secure) to be isolated from more stable engineering systems. Most companies have a separate “lab net” for this purpose. Access to these systems from outside engineering via `FTP`, `telnet`, and other insecure methods should be blocked. Offer to help the engineers set up `SSH` instead.

Sales and marketing types interact with outside systems more frequently than other departments, and these people tend to be less technically sophisticated. This is a good reason to isolate them on a separate network. It would be a good idea to block incoming `FTP` and `telnet` to each of your organization’s different networks. A common solution is to have a system for “bouncing files” off. Thus, to copy a file from system $A$ to system $B$, someone on system $A$ would `FTP` said file to the bounce system in a public area.

Then someone on system $B$ would initiate a `FTP` connection to the bounce system and download the file. `FTP` to the bounce system from outside the company would be blocked, and a daily `find` command would remove all files in the public `FTP` area that were older than, say, a day. This “bounce” system and the appropriate firewall rules prevent a system, possibly a compromised system, from breaking other systems because “you can’t get there from here.” See “Intracompany Firewalls to Contain Fires” on page 78 for details.
