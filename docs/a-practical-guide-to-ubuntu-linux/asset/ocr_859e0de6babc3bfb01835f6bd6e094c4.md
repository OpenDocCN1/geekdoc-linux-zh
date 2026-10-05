# HOST SECURITY 1119

+   Mount filesystems other than and /usr nosuid to prevent setuid programs from executing on this filesystem. For example:

```
/dev/sda4      /var      ext4  nosuid 0 0
/dev/sda5      /usr/local ext4  nosuid 0 0
```

+   Use a barrier or firewall product between the local network and the Internet. Valuable mailing lists cover firewalls, including the comp.security.firewalls newsgroup and the free firewall Web site (www.freefire.org). Ubuntu Linux includes firestarter (page 864), gufw (page 876), and iptables (page 880), which allow you to implement a firewall.

# HOST SECURITY

Your host must be secure. Simple security steps include preventing remote logins and leaving the /hosts.equiv and individual users' ~/hosts empty (or not having them at all). Complex security steps include IPSec for VPNs between hosts. Many other security measures, of which are discussed in this section, all for-where between these extremes. See Table C-1 on page 1124 for relevant URLs.

+   Although potentially tricky to implement and manage, intrusion detection systems (IDS) are an excellent way to keep an eye on the integrity of a device which it runs. An IDS can warn of possible attempts to subvert the security of the host on which it runs. The great-grandaddy of systems is triwire. This host-based system check modification times and integrity of files by using strong algorithms (cryptographic checksums or signatures) that can detect the most minor modifications. A commercial version of triwire is also available. Another commercial IDS is Dragonsquire. Other free, popular, and flexible IDS include samhain and AIDE. The two IDS offer even more features and means of remaining invisible to users than triwire does. Commercial IDS that are popular in enterprise environments Cisco Secure IDS (formerly NetRanger), Elasticsearch Dragon, and ISS RealSecure.

+   Keep Ubuntu systems up-to-date by downloading and installing the latest updates. Use the Update Notifier to update the system regularly (page 112). You can set the system up to automatically install security updates using the Software Sources, Updates tab (page 131).

+   Complementing host-based IDS are network-based IDS. They monitor the network and nodes on the network and report suspicious occurrences (attack signatures) by user-defined alerts. These signatures can be matched based on known worms, overflow attacks against programs, or unauthorized scans of network ports. Such programs such as snort, klaxon, and NFR are used in this capacity. Commercial programs such as DragonSentry, also fill this role.