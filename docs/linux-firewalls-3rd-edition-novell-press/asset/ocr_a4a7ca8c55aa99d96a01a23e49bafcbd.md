Refer to your switch's documentation for more information. For example, Cisco Catalyst switches call this feature "Switched Port Analyzer," or SPAN. More information on SPAN can be found at http://www.cisco.com/warp/public/47/3/4/1.html.

Regardless of where the traffic originates, if it comes into the interface where the sniffer is running, the traffic can be captured. The key, at a network level, is to place sniffers and the related intrusion detection software in the right locations. For host-based traffic sniffing, the placement of the sniffer is obvious, on the host itself.

# Sniffer Placement

The placement of network sniffers and traffic-analysis software is key to successfully analyzing the traffic. In a switched network, the switch needs to be configured to mirror all traffic out the sniffer's switch port. Chapter 11 discusses the placement of sniffers. In essence, I recommend placing them in as many points as you can, notably near termination points such as firewalls.

# ARPWatch

Another item to be discussed in Chapter 11 is ARPWatch. ARPWatch is software to watch for new network devices on the network. ARPWatch can be helpful for auditing the devices on the network, especially wireless networks.

# Rootkit Checkers

A rootkit is a piece of software or a grouping of software that attempts to exploit one or more vulnerabilities with the goal of enabling an attacker to gain elevated privileges or perform any other type of attack against the target. Frequently, rootkits are used by less skilled attackers who use the software built by another attacker but don't really understand the underlying exploit; they're just interested in the results.

Many rootkits not only run the initial exploit to give the attacker root privileges but also attempt to mask or hide the fact that an attack has been launched. They do this by deleting log files or certain entries from log files, planting trojan-horse versions of programs, and employing other means. There is also nothing stopping an attacker from chaining rootkits together for multiple levels of deception and possible exploit.

Like network-centric attacks, rootkits frequently have signatures or leave other traces that identify them. These traces and signatures might be the aforementioned removal of log files, the presence of one or more processes, or other changes to the system that are specific to the rootkit software or the exploit.