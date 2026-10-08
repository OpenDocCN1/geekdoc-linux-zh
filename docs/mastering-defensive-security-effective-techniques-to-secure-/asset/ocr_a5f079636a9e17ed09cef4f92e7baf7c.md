+   - System malfunction (cyberwarfare)
- System disruption (hacktivism)
- System damage

# Malware connections

Another key aspect of malware analysis is determining who created the malware and where the exiltrated data is going.

This is important for two main reasons. The first is about the legal aspect, because in most countries, the distribution of malware is a crime, and therefore identifying the group that is trying to compromise your systems is vital.

The second reason is about using this information to block and blacklist the Internet Protocol (IP) addresses used by the malware that will prevent further attacks.

Additionally, this data (IPS, server names, and so on) can be used by open source (crowdsource) systems to prevent attacks in other companies and industries.

Have a look at the following screenshot:

![](bbox=[0.119, 0.506, 0.839, 0.673])

Figure 14.1 - IP blacklisting

As seen in the preceding screenshot, blacklisting IP addresses may help to stop an ongoing attack, but also may prevent future attacks from the same group. It is also important to remember that blacklisting will also prevent a command-and-control (C&C) attack.

# Malware backdoors

A common characteristic of malware is to create backdoors. While the usage and objectives of those backdoors may vary, it is very important to determine any trail of backdoors to reduce the possibility of further infections or data compromise.