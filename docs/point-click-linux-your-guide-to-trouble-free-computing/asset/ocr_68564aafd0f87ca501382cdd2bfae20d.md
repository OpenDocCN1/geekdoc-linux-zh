# NeTraverse Win4Lin

While CrossOver Office runs some Windows applications in Linux, Win4Lin actually runs Windows in Linux, which means virtually all Windows applications work well. One big catch is that in order to use Win4Lin you need to have a copy of Windows around that you can legally load on your Linux computer. The other big Win4Lin catch is that as late as mid-2004 it would still only work with Windows 95, 98, and ME, but you may want to check MEPIS.org to see if this has changed since then. Last we heard while writing this book, a new XP-enabled version of Win4Lin was scheduled for release by the end of 2004.

![](bbox=[0.65, 0.13, 0.93, 0.4])

There are some special Linux kernel modifications needed to run Win4Lin, but they're already built into MEPIS so installation is painless, and installing Windows programs on Windows running on Win4Lin under Linux is faster than installing them in a regular Windows computer because rebooting Windows in Win4Lin is much faster than booting Windows all by itself.

# Networking with Windows Machines Using Samba

By Jem Matzan

Even if we don't use any Windows programs ourselves, we may still need to work with Windows computers on a home or office network. We do this with a program called Samba that lets us read Windows files directly from our Linux computer.

# Samba: The Server Message Block Client

In order for Linux to access a Windows network, it must use the SMB (Server Message Block) network file-sharing protocol. SimplyMEPIS uses a program called Samba to access Windows shares using that protocol.