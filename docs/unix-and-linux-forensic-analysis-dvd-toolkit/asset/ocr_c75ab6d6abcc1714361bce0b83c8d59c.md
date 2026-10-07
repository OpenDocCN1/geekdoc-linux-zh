# The Hacking Top 10 • Chapter 5

# Figure 5.4 Nmap Scan

![](bbox=[0.139, 0.105, 0.861, 0.478])

As you can see, the target is running some version of Windows, with ports 135, 139, 445, and 912 open. The netBIOS ports are understandable, considering I am running Windows XP SP2, but what is the deal with port 912? Further investigation of that port shows that the deal is the VMware Workstation 6. From this brief, albeit noisy scan, I now know the OS of the target host, as well as the ports that are available to include at least one running application. Based on this information, an attacker can begin to formage an exploitation plan to gain access to the target host. So if you ever come across entries like this in a case, pay special attention to hosts scanned more than once. It is possible that the first scan could have been a sweep, the second OS detection, and a third service identification. If there are several systems that are appearing in the logs, what do they have in common? Do they have the same OS? Are they running similar services? Use that information to ascertain what the intruder may be.

This is one example of a scan being executed with nmap. As I previously stated, there are literally hundreds of variables that could be used to acquire information