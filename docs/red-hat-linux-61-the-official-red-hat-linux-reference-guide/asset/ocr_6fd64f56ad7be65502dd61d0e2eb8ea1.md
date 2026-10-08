# Chapter 19. Tripwire

Tripwire integrity assurance software monitors the reliability of critical system files and directories by identifying changes made to them. It does this through an automated verification regimen run at regular intervals. If Tripwire detects a monitored file has been changed, it notifies the system administrator via email. Because Tripwire can positively identify files that have been added, modified, or deleted, it can speed recovery from a break-in by keeping the number of files which must be restored to a minimum. These abilities make Tripwire an excellent tool for system administrators seeking both intrusion detection and damage assessment for servers.

Tripwire works by comparing files and directories against a database of file locations, dates they were modified, and other data. This database detects baselines — which are snapshots of specified files and directories at a specific point in time. The contents of the database should be generated before the system is at risk of intrusion, meaning before it is connected to the network. After creating the baseline database, Tripwire compares the current system to the baseline and reports any modifications, additions, or deletions.

While Tripwire is a valuable tool for auditing the security state of Red Hat Linux systems, Tripwire is not supported by Red Hat, Inc. If you need more information about Tripwire, a good place to start is the project's website located at http://www.tripwire.org.

# 19.1. How to Use Tripwire

The following chart illustrates how Tripwire works:

![](bbox=[0.095, 0.515, 0.475, 0.885])

Figure 19-1. Using Tripwire