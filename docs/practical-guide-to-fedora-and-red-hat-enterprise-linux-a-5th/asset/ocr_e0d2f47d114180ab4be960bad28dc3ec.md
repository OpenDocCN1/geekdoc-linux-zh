nobody = guest
sam = sams
Default: no map
Fedora/RHEL: /etc/samba/smbusers

# LOGGING PARAMETERS

**log file** The name of the Samba log file. Samba replaces %m with the name of the client system, allowing you to generate a separate log file for each client.
Default: none
Fedora/RHEL: /var/log/samba/%m.log

**log level** Sets the log level, with 0 (zero) being off and higher numbers being more verbose.
Default: 0 (off)

**max log size** An integer specifying the maximum size of the log file in kilobytes. A 0 (zero) specifies no limit. When a file reaches this size, Samba appends a .old to the filename and starts a new log, deleting any old log file.
Default: 5000
Fedora/RHEL: 50

# BROWSER PARAMETERS

The *domain master browser* is the system that is responsible for maintaining the list of machines on a network used when browsing a Windows Network Neighborhood or My Network Places. SMB (page 1106) uses weighted elections every 11–15 minutes to determine which machine will be the domain master browser.

Whether a Samba server wins this election depends on two parameters: First, setting **domain master** to YES instructs the Samba server to enter the election. Second, the **os level** determines how much weight the Samba server’s vote receives. Setting **os level** to 2 should cause the Samba server to win against any Windows 9x machines. NT Server series domain controllers, including Windows 2000, XP, and 2003, use an **os level** of 32. The maximum setting for **os level** is 255, although setting it to 65 should ensure that the Samba server wins.

**domain master** YES causes nmbd to attempt to be the domain master browser. If a domain master browser exists, then local master browsers will forward copies of their browse lists to it. If there is no domain master browser, then browse queries may not be able to cross subnet boundaries. A Windows PDC (Primary Domain Controller) will always try to become the domain master and may behave in unexpected ways if it fails. Refer to the preceding discussion.
Default: AUTO

**local master** YES causes nmbd to enter elections for the local master browser on a subnet. A local master browser stores a cache of the NetBIOS (page 1095) names of entities on the local subnet, allowing browsing. Windows machines automatically enter