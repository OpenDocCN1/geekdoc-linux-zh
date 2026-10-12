# ### 22.4 Samba

Samba (so called because it provides SMB file and printer sharing) is a superb free software implementation of Windows Networking for Linux/UNIX. It includes:

+   - NetBIOS name resolution
+   - SMB file sharing
+   - domain authentication
+   - network browsing.

Both client-side and server-side are included, so you can:

+   - access files on Microsoft Windows PCs from your Linux machines
+   - access files on your Linux machines from Microsoft Windows PCs.

This allows you to share the same data to both Linux and Windows users, without having to duplicate them. If you keep your data on Linux Samba servers, then you don’t need to install any extra software on any of your desktop machines (Figure 22.4). Windows PCs see the Samba server as a Windows Networking file server, included in their browse list as normal, and Linux users can access the server using NFS (Module 17.14). In Appendix 26 we explain how we use this type of configuration to share our central archive of software to all the machines on our network.

![](bbox=[0.12, 0.45, 0.88, 0.71])

As well as saving you effort and money – not having to buy or install client software for your desktops – we’ve found this approach also leads to more reliable networks: the less software you have to install on Windows machines the better, especially “intrusive” networking software that has to work at a low level within the operating system. An alternative approach used widely in the past was to install commercial, third-party NFS software on the Windows PCs. While this works, it can be expensive, and we’ve often found that low-level software like this can be troublesome, especially on earlier versions of Windows.

Our experiences with Samba have been very good: it works reliably, it performs well, the documentation is helpful (although written mostly for a technical audience), and it has some useful tools. Surprisingly, we’ve found it easier to gain an understanding of Windows