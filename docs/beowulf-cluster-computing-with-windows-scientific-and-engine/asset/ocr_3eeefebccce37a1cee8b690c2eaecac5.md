# # 4 Windows 2000

David Solomon

This chapter introduces the architecture of the Windows 2000 operating system. Before delving into the internals of the system, let’s review the origin of the system and its various flavors.

# ## 4.1 Introduction to Windows 2000

Windows 2000 is actually the fifth version of the Windows NT-based operating system family. The original version, Windows NT 3.1, was released in 1993. From the initial announcement of Windows NT, Microsoft has always made it clear that this operating system was to be their single strategic operating system platform for the future. The next version, Windows XP, is the first NT-based release to be aimed not just at the business desktop and server market, but also at the consumer or home market. It replaces Windows 95, Windows 98, Windows Millennium Edition, and Windows 2000.

NT stands for “new technology.” While NT represents a modern 32-bit operating system platform (and with Windows XP, a 64-bit version is available as well), it is not “new” when compared with most modern-day Unix systems. The core system calls and networking capabilities are quite similar.

There are four editions of Windows 2000: Windows 2000 Professional, Windows 2000 Server, Windows 2000 Advanced Server, and Windows 2000 Datacenter Server. These editions differ by

+   - the number of processors supported,
+   - the amount of physical memory supported,
+   - the number of concurrent network connections supported, and
+   - layered services that come with Server editions that don’t come with the Professional edition.

These differences are summarized in Table 4.1.

# ## 4.2 Operating System Model

To provide a framework for understanding Windows 2000, let’s first review the requirements and goals that shaped the original design and specification of the