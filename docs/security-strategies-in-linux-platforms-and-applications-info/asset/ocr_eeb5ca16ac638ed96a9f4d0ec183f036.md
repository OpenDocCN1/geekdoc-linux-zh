# PART 3 | Building a Layered Linux Strategy

A sampling of live media with penetration testing tools includes the following:

+   - Per the BackTrack Web site, "BackTrack has been customized down to every package, kernel configuration, script and patch solely for the purpose of the penetration test.\ While it was originally built on the Slack Linux distribution, for Ubuntu. For more information, see http://backtrack-linux.org/
- Knppix Security Tools Distribution (STD)—The Knppix STD is based on but not affiliated with Knppix. It includes tools for forensics, IDSs, password checkers, protocol analyzers, and variety of vulnerability-assessment tools. For more information, see http://s-t-dorg.
- Network Security Toolkit (NST)—Based on not affiliated with Fedora, the Network Security Toolkit includes a majority of the top 100 security tools listed at http://sectools.org/. For more information, see http://networksecuritytoolkit.org.

# Best Practices: Testing and Reporting

When testing a Linux system, it's important to test every part of a layered defense. Because some tests may require temporarily disabling defenses, it's appropriate to withdraw a system from production before running tests. Open ports on a system should appear different inside a firewall from outside. Tests of TCP Wrappers depend on the rules configured in the /etc/hosts. A low and /etc/hosts deny files. Tests of some services may be specific to the limitations configured within the configuration for that service. Tools such as the John Ripper help identify passwords that are too simple. Be sure to re-enable any disabled services after tests are complete.

Services aren't accessible over open network ports. It's important to know what network ports are open on local systems to make sure that the only ports that are open are those required for local services. Tools that can help check for network ports include telnet, netstat, lsof, and nmap. The nmap command is especially versatile, as it can scan different ports, protocols, and operating systems on a variety of targets.

Several tools can help you check for unauthorized changes to key files. The rpm -Va and debsums command checks them against installed files. Because even normal changes to configuration files are highlighted, more precise tools are needed. Two options to that are de Tripwire and AIDE.

Some systems have so many security rules, they're too difficult for people to use. That can lead to security problems. For example, when password policies are too strict, users who have trouble remembering their exotic passwords may write them down at their workstations. Password policies can be managed with the change command; access can be regulated with the PAM files.

Several options are available for virtual machine hardware, from VMware to Virtualbox. The emerging standard for an open source virtual machine manager is KVM. While such virtual machines use large files that simulate hard disks, the contents of these files change frequently. So intrusion detection tools are important to monitor the integrity of such systems.

![](bbox=[0.19, 0.956, 0.235, 0.978])