# Chapter 13 • IMPLEMENTING SYSTEM SECURITY

# Detecting Suspicious Activity

How do you know if you are under attack? Has somebody gained root access to your system? If these are questions that keep you at night, you are not alone. While several technical solutions help you detect intrusions, your own familiarity with your system is one of your strongest tools for detecting suspicious activity. As you work with a system, you become familiar with that of each directory, the rough capacity of its file systems, its typical interactive performance, normal load averages, and the names of processes that run on it. When you know your system well, you notice deviations from these "norms".

Take some time each day to be proactive and check up on your systems, run df to look at system capacities, uptime to look at load averages, and ps to see what processes are running. If load averages are higher than usual, you see a system that is taking up more space than usual, or ps lists a process name that you have never seen before.

A system administrator should have the "guilty until proven innocent" attitude towards his her systems. If something seems suspicious, it probably does not belong on your system. It can be much harder to determine on login servers where hundreds or thousands of users can run any number of different programs, even on those systems you can get a feel for other characteristics, such as load average and file system usage.

# Configuration Errors

Unix is an extraordinarily flexible operating system; it can be configured in any number of ways and can run third-party software that is also highly configurable. With all of configuration going on, it isn't difficult for even the best administrator to slip up and create a configuration that exposes a system to potential attacks.

# Use Effective Change Management Procedures

Effective change management can drastically reduce the number of human errors in configurations by requiring more than one person to audit any changes that occur. Chapter 14, "Internal Communication," discusses change management in more detail.

This type of human error is one of the leading causes of system insecurities. For example, if you needed to put a "+" in /etc/hosts.allow to allow remote access temporarily but forgot to remove it, you have just allowed remote user to log in to any account without a password (assuming login is enabled inetd.conf).

Unix configuration involves a large number of files, and there are several programs that can help you check those files for inconsistencies. Most widely used and generally applicable program for uncovering configuration errors is COPS, the Computer Oracle and Password System, available from ftp://coast.cs.purdue.edu/pub/tools/scanners/cops. A general overview is available at http://www.fish.com/cops/overview.html.

![](bbox=[0.105, 0.582, 0.165, 0.618])