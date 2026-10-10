![](bbox=[0.13, 0.05, 0.81, 0.4])

**Figure 5.11 SAFEsuite.**

> **Hacker's Note**
> SAFEsuite can be evaluated on this book’s CD.

# Security Administrator's Tool for Analyzing Networks Successor SAINT

**Platforms:** Solaris, Linux, IRIX

The Security Administrator’s Tool for Analyzing Networks (alias: SATAN) was written by Dan Farmer and Wiete Vegema, and is advertised as a tool to help system administrators. According to Muffy Barkocy, a SATAN consultant, the program was developed out of the realization that computer systems are becoming more dependent on the network, and at the same time becoming more vulnerable to attack via that same network. SATAN recognizes and reports several common networking-related security problems, without actually exploiting them. For each type of problem found, SATAN offers a tutorial that explains the problem and its potential impact. The tutorial also explains how to remedy the problem, whether, for example, to correct an error in a configuration file, install a patch or bug fix from the vendor, use other means to restrict access, or simply disable a service.

SATAN collects information that is available to everyone with access to the network. With a properly configured firewall in place, there should be near-zero information accessible by outsiders. Limited research conducted by Muffy, found that on networks with more than a few dozen systems, SATAN would inevitably find problems. Keep in mind, however, that the intruder community has been exploiting these problems for a long time.

SATAN was written primarily in Perl and C with some HTML front ends for management and reporting. The kernel is tarred and zipped, and is compatible only with most UNIX flavors. SATAN scans focus on, but are not limited to, the following daemon vulnerabilities:

+   - FTPD