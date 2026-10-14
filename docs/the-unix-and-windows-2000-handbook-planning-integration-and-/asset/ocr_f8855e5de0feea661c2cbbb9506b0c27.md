that help to determine that your security has been breached are called intrusion detection system (IDS) tools. IDS tools function by gathering data from within your infrastructure, and then they perform an analysis to determine if there is a security breach. This analysis can function in two ways:

+   - **Post-mortem**—These tools assume that an intrusion has occurred and the system administrator wants to determine what damage has occurred.
+   - **Real-time**—The IDS tool attempts to detect an intrusion while it is occurring. When an intrusion is detected, the IDS tool sends an alarm to the system administrator and possibly launches a counter-attack. Such counter-attacks can be a firewall reconfiguration, the blocking of a user account, or of a system shutdown.

An IDS tool can perform its analysis by:

+   - Ongoing monitoring of user and system activity.
+   - Checking the integrity of critical components (such as binaries and configuration files or data).
+   - Trying to recognize a known attack by using pattern recognition.
+   - Performing a statistical analysis of user and system activity and generating alerts on suspicious readings.
+   - Checking the activity of users to determine policy violations.

The various IDS tools can be classified into the following categories:

+   - **Network intrusion detection system (NIDS)**—A NIDS act like a network sniffer. It captures all network traffic and analyzes it for network-based attacks, such as denials of service. Because of its design, a NIDS can monitor many machines for remote intrusion.
+   - **Host-based IDS**—A host-based IDS is different from a NIDS in that it monitors a single host by gathering logs, process information, and user activity. A host-based IDS can try to detect an intrusion by either performing attack recognition or statistical recognition (any unusual activity is detected). Among the different host-based IDS tools, the most common are:
+     - Log monitors, whose role is to analyze logs produced on hosts and look for patterns that may suggest that a host is under attack.
+     - Deception systems (also known as decoys or honeypots), which simulate a well-known security hole that can be exploited. They are used to entrap an intruder, study their activity, and give the administrator time to determine the identity of the intruder.