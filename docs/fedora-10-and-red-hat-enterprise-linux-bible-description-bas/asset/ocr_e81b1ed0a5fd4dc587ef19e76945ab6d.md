# 986 Part IV: Fedora and RHEL Network and Server Setup

![](bbox=[0.131, 0.083, 0.672, 0.502])

**Figure 26-1:** Configure your Mac OS X network interface to connect to Linux servers.

# Using AppleTalk (netalk) from Mac OS X

AppleTalk is the traditional set of protocols used by Apple computers to share files and printers over a LAN. Although Mac OS X can support Samba file sharing, AppleTalk is still a familiar way for Mac users to get to networked printers and files.

Fedora and RHEL include a software package called netatalk that you can use to configure Linux as an AppleTalk file and printer server. To a Mac client, the netalk server looks different than any other AppleTalk server.

> CROSS-REFERENCE: Refer to the "Setting up the netatalk server" section later in this chapter.

To access a shared directory from an AppleTalk server, click Go in the Finder bar at the top of the screen, and then select Connect to Server. The Connect to Server window appears, as shown in Figure 26-2.