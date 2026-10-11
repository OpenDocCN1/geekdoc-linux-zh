well as the capability to back up and manage files more intuitively, advantages that often outweigh the performance advantages of SAN. Additionally, SAN cabling restrictions (and concerns about security when accessing data over corporate networks) can limit the appeal of SANs to large server rooms.

# # The Network File System Protocol

Network file system protocols come in all shapes and sizes. Some require complex clients to manage complex state information (such as AFS), whereas others are idempotent (stateless), such as NFS version 3. They vary from OS/2-centric (such as SMB) to Windows-centric (such as CIFS) and UNIX-centric (such as NFS). They vary in their security models, performance, and, of course, complexity. SANs move data as if it were blocks on disk, whereas most network file systems move data based on the filename or file identifier.

Making sense of this maze of protocols requires looking back and categorizing the protocols into families. The following list groups related network file system protocols into families to make it easier to understand their characteristics:

# ## Major Network File System Families

+   * HTTP — WebDAV
+   * SMB — CIFS
+   * NCP (Netware Core Protocol)
+   * NFSv2 — NFSv3 — WebNFS — NFSv4 — DAFS
+   * AFS — DCE/DFS, AFS — Coda — Intermezzo
+   * AFP
+   * GFS, GPFS, and hybrid network file systems

A more detailed description of the more popular network file systems follows. The file systems are listed in order of the approximate size of their installed base:

+   * **SMB/CIFS.** This network file system was invented by Dr. Barry Feigenbaum of IBM in the early 1980s, was extended heavily by Microsoft, and then was renamed CIFS in the late 1990s by Microsoft. This protocol is the default network file system on most versions of Windows (and even OS/2 and DOS), and most modern operating systems support it. The 2.6 Linux kernel includes two client implementations: the legacy smafs and the newer CIFS VFS client, which will eventually replace smafs. There are also user space SMB file system tools, which are commonly used on Linux (although, not part of the kernel