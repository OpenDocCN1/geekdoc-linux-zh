Ping statistics for 192.168.0.21:

	Packets: Sent=4, Received=4, Lost=0 (0% loss),

Approximate round trip times in milli-seconds:

	Minimum=2ms, Maximum=3ms, Average=2ms

On the Linux server, append a rule to the INPUT chain to drop ICMP packets from
192.168.0.3. The following command will be applied:

*iptables -A INPUT -s 192.168.0.3 -p icmp -j DROP*

The *-A INPUT* designates that this rule will be appended to the INPUT chain. The *-s
* **192.168.0.3** *is the source host the rule applies to. The* **-p icmp** *indicates that the icmp pro-
tocol is affected. The* **-j DROP** *says that if the rule is a match, drop the packet.*

Try the ping after completing this rule. The following ping shows the result:

Pinging 192.168.0.21 with 32 bytes of data:

Request timed out.

Request timed out.

Request timed out.

Request timed out.

Ping statistics for 192.168.0.21:

Packets: Sent=4, Received=0, Lost=4 (100% loss),

To remove the rule we just added, use the following command:

*iptables -D INPUT -s 192.168.0.3 -p icmp -j DROP*

The *-D option uses the same rule as a match to remove the rule from the INPUT*
*chain. To use this command, the rule must match the original exactly. You can also use the*
*number of the rule in the list. To find which number position the rule is in, use the* *-L option*
*to list the rules. The* **iptables** *command sequence lists all the chains:*

Chain INPUT (policy ACCEPT)

target prot opt source destination

RH-Lokkit-0-50-INPUT all -- anywhere anywhere

DROP icmp -- engle-ee102 anywhere

Notice that the destination is replaced with the name of the machine instead of the IP
address. This is the name found in the */etc/hosts* file. To show the counters as well, use the
*-v option.*

*iptables rules are applied in the order of appearance in the chain. If you want to give*
*a host access to specific protocols but deny it access to all the rest, you should enter the AC-*
*CEPT rules first and then the DROP rule. If the DROP appears before the ACCEPT, no*
*packets will get through.*

# FILE SYSTEM SECURITY

File system security is not put in place just to deter the unauthorized user; you have files on
your system that you do not want local users to view or execute as well. For example, if
your system contains payroll information for a company, you do not want everyone to be
able to view it. Your users will want to know that their files are safe from others viewing,
executing, changing, or copying. The main tool to secure the file systems on a computer is
file permissions, discussed in Chapter 4.

# File Permissions

Files in Linux have three types of access—read, write, and execute. These access permis-
sions are applied to the owner of the file, the group the owner belongs to, and everyone else.
The file permissions can be viewed by displaying a long list of a directory. The following
is a directory listing of *jsmith.*