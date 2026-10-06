Biometric locks to all server rooms, or equipment storage rooms. Such locks are triggered by a fingerprint scan, and the identity of the person as well as the time they entered the room are recorded.

All visitors to the building are logged in (both their entry and exit time) and are escorted by an employee at all times.

All bags are inspected when personnel leave, or at least bags are inspected at random.

No portable devices that might record data are allowed on the premises. This includes USB drives, camera phones, or any device that might copy data or record screen.

All printing is logged. Who printed, the time the printing occurred, the document name, and the document size.

All copying is logged, similarly to printing.

If you are in a situation that demands a greater than normal security level, these measures may be considered.

# Probing the Network

Perhaps the most critical step in assessing any network is to probe the network for vulnerabilities. This means using various tools to scan your network for vulnerabilities. Some network administrators skip this step. You audit policies, check the firewall logs, check patches, and so on. However, the probing tools discussed in this section are the ones that most hackers use. If you want to know how vulnerable your network is, it is prudent to try the same tools that an intruder would use. In this section we review the more common scanning/probing tools. There are essentially three types of probes that are usually done. These are the same types of probes that skilled hackers use to evaluate your network:

+   Port scanning: This is a process of scanning the well-known ports (there are 1024) or even all the ports (there are 65,535) and seeing which ports are open. Knowing what ports open tells you about a system. If you see that 160 and 161 are open ports tells you that the system is using SNMP. From the perspective of a network administrator, there should be no ports that are not necessary.

+   Enumerating: This is a process whereby the attacker tries to find out what is on the target network. Items such as user accounts, shared folders, printers, and so on are sought after. Any of these might provide a point of attack.

+   Vulnerability assessment: This is the use of some tool to seek out known vulnerabilities, or the attacker might try to manually assess vulnerabilities. Some outstanding tools are available for vulnerability assessment.