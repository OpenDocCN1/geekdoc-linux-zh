max log size An integer specifying the maximum size of the log file in kilobytes. A 0 (zero) specifies no limit. When a file reaches this size, Samba appends .old to the filename and starts a new log, deleting any old log file.
Default: 5000
Ubuntu: 1000

# **BROWSER PARAMETERS**

The *domain master browser* is the system responsible for maintaining the list of machines on a network used when browsing a Windows Network Neighborhood or My Network Places. SMB (page 1172) uses weighted elections every 11–15 minutes to determine which machine is the domain master browser.

Whether a Samba server wins this election depends on two parameters:

+   • Setting **domain master** to YES instructs the Samba server to enter the election.
+   • The **os level** determines how much weight the Samba server’s vote receives.

Setting **os level** to 2 should cause the Samba server to win against any 9x machines. NT Server series domain controllers—including Windows 2000, XP, and 2003—use an **os level** of 32. The maximum setting for **os level** is 255, although setting it to 65 should ensure that the Samba server wins.

**domain master** YES causes **nmbd** to attempt to be the domain master browser. If a domain master browser exists, then local master browsers will forward copies of their browse lists to it. If there is no domain master browser, then browse queries may not be able to cross subnet boundaries. A Windows PDC (primary domain controller) will always try to become the domain master browser and may behave in unexpected ways if it fails. Refer to the preceding discussion for more information.
Default: AUTO

**local master** YES causes **nmbd** to enter elections for the local master browser on a subnet. A local master browser stores a cache of the *NetBIOS* (page 1161) names of entities on the local subnet, allowing browsing. Windows machines automatically enter elections; for browsing to work, the network must have at least one Windows machine or one Samba server with **local master** set to YES. It is poor practice to set **local master** to NO. If you do not want a computer to act as a local master, set its **os level** to a lower number, allowing it to be used as the local master if all else fails.
Default: YES

**os level** An integer that controls how much Samba advertises itself for browser elections and how likely **nmbd** is to become the local master browser for its workgroup. A higher number increases the chances of the local server becoming the local master browser. Refer to the discussion at the beginning of this section for more information.
Default: 20

**preferred master** YES forces **nmbd** to hold an election for local master and enters the local system with a *slight* advantage. With **domain master** set to YES, this parameter helps ensure the local Samba server becomes the domain master. Setting this parameter to YES on more than one server causes the servers to compete to become master, generating a