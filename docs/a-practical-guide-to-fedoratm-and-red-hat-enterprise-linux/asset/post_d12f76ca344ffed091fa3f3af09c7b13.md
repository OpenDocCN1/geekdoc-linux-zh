
commonly used to establish a secure point-to-point virtual network (VPN, page 1280) that allows two hosts to communicate securely over an insecure channel, such as the Internet. This protocol provides integrity, confidentiality, authenticity, and flexibility of implementation that supports multiple vendors.

IPSec is an amalgamation of protocols (IPSec = AH + ESP + IPComp + IKE):

- **AH (Authentication Header)**—A cryptographically secure, irreversible *checksum* (page 1242) for an entire packet. AH guarantees that the packet is authentic.
- **ESP (Encapsulating Security Payload)**—Encrypts a packet to make the data unreadable.
- **IPComp (IP Payload Compression)**—Compresses a packet. Encryption can increase the size of a packet, and IPComp counteracts this increase in size.
- **IKE (Internet Key Exchange)**—Provides a way for the endpoints to negotiate a common key securely. For AH to work, both ends of the exchange device must use the same key to prevent a “man in the middle” (see the tip on page 1160) from spoofing the connection.

While IPSec is an optional part of IPv4, IPv6 (page 293) mandates its use.

## NETWORK SECURITY GUIDELINES

The following list of general guidelines for establishing and maintaining a secure system is not a complete list, but rather is meant as a guide.

- Fiberoptic cable is more secure than copper cable. Copper is subject to both active and passive eavesdropping. With access to copper cable, all a data thief needs to monitor your network traffic is a passive device for measuring magnetic fields. In contrast, it is much more difficult to tap a fiberoptic cable without interrupting the signal. Sites requiring top security keep fiberoptic cable in pressurized conduits, where a change in pressure signals that the physical security of the cable has been breached.
- Avoid leaving unused ports available in public areas. If a malicious user can plug a laptop into the network without being detected, you are at risk of a serious security problem. Network drops that will remain unused for extended periods should be disabled at the switch, preventing them from accepting or passing network traffic.
- Use the latest in wireless encryption. At the time of this writing, WEP is totally broken and WPA with TKIP is seriously flawed. WPA2 with AES is generally believed to be relatively secure.
- Many network switches have provisions for binding a hardware address to a port for enhanced security. If someone unplugs one machine and plugs in another machine to capture traffic, chances are that the second machine will have a different hardware address. When it detects a device with a different hardware address, the switch can disable the port. Even this solution is no guarantee, however, as some programs enable you to change or mask the hardware address of a network interface. This setup can be inconvenient when you need to swap out a machine for repair.

## Install a small kernel and run only the programs you need

Security Linux systems contain a huge number of programs that, although useful, significantly reduce the security of the host. Install the smallest operating system kernel that meets your needs. For servers, install only the needed components and do not install a graphical interface. Fewer packages mean fewer urgent security patches. Users might require additional packages.

- Do not allow NFSv3 or NIS access outside the local network. Otherwise, it is a simple matter for a malicious user to steal the password map. Default NFSv3 security is marginal to nonexistent (a common joke is that NFS stands for No File Security or Nightmare File System) so such access should not be allowed outside your network to machines you do not trust. Versions of NFS for Linux that support much better authentication algorithms are available. Use IPSec, NFSv4 (which includes improved authentication), or firewalls to provide access outside of the local domain. Kerberos, when combined with NFSv4 or NFSv3 provides very good security, but configuring Kerberos requires a book unto itself.
- Support for VPN configuration is often built into new firewalls or provided as a separate product, enabling your system to join securely with the systems of your customers or partners. If you must allow business partners, contractors, or other outside parties to access local files, consider using a secure filesystem, such as NFS with Kerberos (page 1257), secure NFS (encrypts authentication, not traffic), NFS over a VPN such as IPSec, or cfs (cryptographic filesystem).
- Specify /usr as readonly (ro) in /etc/fstab. Following is an example of such a configuration:

  ```
  /dev/sda6 /usr ext2 ro 0 0
  ```

  This approach is not suitable for all operating systems, or even all Linux distributions. Some applications put changeable files in /usr. Also, this setup entrenches security flaws and makes the system difficult to update.
- Mount filesystems other than / and /usr nosuid to prevent setuid programs from executing on this filesystem. For example:

  ```
  /dev/sda4 /var ext4 nosuid 0 0
  /dev/sda5 /usr/local ext4 nosuid 0 0
  ```
- Use a barrier or firewall product between the local network and the Internet. Several valuable mailing lists cover firewalls, including the free firewalls Web site (www.freefire.org). Fedora/RHEL includes firewall-config (page 900) and iptables (page 908), which allow you to set up a firewall.
- Use a program that checks file integrity. Some examples are tripwire, samhain, and AIDE. These tools include a database of checksums of files you want to monitor and alert you when any of the monitored files change.

## HOST SECURITY

Your host must be secure. Simple security steps include preventing remote logins and leaving the /etc/hosts.equiv and individual users’ ~/.rhosts files empty (or not having them at all). Complex security steps include installing IPSec for VPNs between hosts. Many other security measures, some of which are discussed in this section, fall somewhere between these extremes. See Table C-1 on page 1180 for relevant URLs.

- Although potentially tricky to implement and manage, IDSS (intrusion detection systems) are an excellent way to keep an eye on the integrity of a device. An IDS can warn of possible attempts to subvert security on the host on which it runs. The great-granddaddy of intrusion detection systems is tripwire. This host-based system checks modification times and integrity of files by using strong algorithms (cryptographic checksums or signatures) that can detect even the most minor modifications. A commercial version of tripwire is also available. Another commercial IDS is DragonSquire. Other free, popular, and flexible IDSS include samhain and AIDE. The last two IDSS offer even more features and means of remaining invisible to users than tripwire does. Commercial IDSS that are popular in enterprise environments include Cisco Secure IDS (formerly NetRanger), Enterasys Dragon, and ISS RealSecure.
- Keep Fedora systems up-to-date by downloading and installing the latest updates. Use yum to update the system regularly (page 534) or allow the system to update itself every night automatically.
- Complementing host-based IDSS are network-based IDSS. The latter programs monitor the network and nodes on the network and report suspicious occurrences (attack signatures) via user-defined alerts. These signatures can be matched based on known worms, overflow attacks against programs, or unauthorized scans of network ports. Such programs as snort, klaxon, and NFR are used in this capacity. Commercial programs, such as DragonSentry, also fill this role.
- Provided with Fedora/RHEL is PAM, which allows you to set up different methods and levels of authentication in many ways (page 476).
- Process accounting—a good supplement to system security—can provide a continuous record of user actions on your system. See the actconf man page (part of the acct package) for more information.
- Emerging standards for things such as RBAC (Role-Based Access Control) allow tighter delegation of privileges along defined organizational boundaries. You can delegate roles to each user as appropriate to the access required.
