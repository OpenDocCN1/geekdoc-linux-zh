# Chapter 22 Security

The format of an entry in either file is *service: host* or *service: network*. Failed connection attempts are noted in syslog. Connections from hosts that are not permitted to access the service are immediately closed.

Most Linux distributions include `hosts.allow` and `hosts.deny` files by default, which are usually empty. Our other example systems all TCP wrappers as an option after installation.

# Bro: the programmable network intrusion detection system

Bro is an open source network intrusion detection system (NIDS) that monitors network traffic and looks for suspicious activity. It was originally written by Vern Paxson and is available from bro-ids.org.

Bro inspects all traffic flowing into and out of a network. It can operate in passive mode, in which it generates alerts for suspicious activity, or active mode, in which it injects traffic to disrupt malicious activity. Both modes require modification of your site's network configuration.

Unlike NIDSs, Bro monitors traffic flows rather than just matching patterns inside packets. This method of operation means that Bro can detect suspicious activity based on who talks to whom, without matching any particular string or pattern. For example, Bro can

+   - Detect systems used as "stepping stones" by correlating inbound and outbound traffic
- Detect a server that has a back door installed by watching for unexpected connections immediately after an inbound
- Detect protocols running on nonstandard ports
- Report corrected passwords (ignore the incorrect guesses)

Some of these features require substantial system resources, but Bro includes clustering to help you manage a group of sensor machines.

The configuration language for Bro is complex and requires significant coding experience to use. Unfortunately, there is no simple default configuration for a novice to master. Most sites require a moderate level of customization.

Bro is supported to extent by the Networking Research Group of the International Computer Science Institute (ICSI), but mostly it's maintained by the community of Bro users. If you are looking for a turnkey commercial NIDS, you will probably be disappointed by Bro. However, Bro can do things that no commercial NIDS can, and it either supplement or replace a commercial solution in your network.

# Snort: the programmable network intrusion detection system

Snort (snort.org) is an open source network intrusion prevention and detection system originally written by Marty Roesch and now maintained by Sourcefire, a