# Chapter 5 • Attacking and Defending Windows 2000

# Figure 5.23 Disabling SMB and NetBIOS Traffic in Windows 2000

![](bbox=[0.198, 0.11, 0.737, 0.413])

# Local Services

Consider eliminating unnecessary features from the local machine. This should include disabling floppy access and applying the same level of password policy and password complexity on the local machine as is required for network access. Services such as autologon should not be tolerated, and use of network monitoring agents agents and SNMP agents should be tightly controlled. Additionally, most backup operations are conducted on a local level, be sure to split the capability of backup and restore operations to protect against theft of the local machine's data and identity. Consider eliminating the display of the last user name in the logon screen through the Local Security Policy snap-in for the Microsoft Management Console.

# Using Tools and Methodologies to Analyze Weaknesses and Configuration Changes

To finish your work of securing Windows 2000, you must continue to analyze and check for potential weaknesses in your systems. This includes not only forming routine, scheduled checks for vulnerabilities and problems, but continually performing checks to ensure that the fixes and blockades you create don't create other problems or lead to other security holes. To do this, you need to employ tools that allow you to get good reports about what is currently in

![](bbox=[0.068, 0.946, 0.294, 0.971])