> Although we will be discussing ACLs in greater detail later in the book, you should use care when editing an ACL to avoid making very costly mistakes. A simple mistake in modifying an ACL can actually prevent even the administrator from accessing a file or other object (that is, not without a lot of extra work).

# Compression

NTFS, unlike FAT and HPFS, natively supports file compression. It is possible under NTFS to achieve a 2:1 compression ratio. NTFS compression is enabled on a per-directory basis and will affect all files and subdirectories. It is important to remember that enabling compression on a directory does not automatically compress the current data. Only new data written to the directory will be compressed. If you want to compress the current data, you must explicitly do so in the Advanced Directory Properties window. To modify the compression settings for a directory, follow these steps:

+   1. Open the Directory Properties window by right-clicking a directory in Windows Explorer and selecting Properties from the list that appears. The window in Figure 4.7 should appear.
+   2. Click the Advanced button to display the Advanced Attributes window shown in Figure 4.8.

Figure 4.7
The Download directory's Properties window.

![](bbox=[0.22, 0.64, 0.78, 0.93])