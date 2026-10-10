to jump the cursor to a place on the screen other than the next position. There exists an ANSI³ standard describing the control sequences which should be sent for various effects. The DEC VT100 and its successors offer the ubiquitous example of this feature in a terminal, but when the system display screen is used, the kernel must provide this capability.

# ## 7.3 File Management

Linux does not impose structure on its files. Any such structure is supported only through run-time libraries and application code.

We have seen a few cases where the operating system kernel “peeks” inside a file:

+   - it looks at the magic word of an executable to determine how the file is to be executed or interpreted,
+   - it can develop a file system inside a file using some experimental modules, and
+   - it can support compressed and encrypted files using other experimental modules.

# ### 7.3.1 Database

Database implementations require some kind of mechanism to ensure mutually exclusive access to records. Some kernels offer record locking, but Linux does not. Instead, Linux offers semaphore operations from which any kind of mutual exclusion system can be built.

# ### 7.3.2 Version Control

Some file systems have a built-in mechanism to track file versions. The FILES-11 used in RSX-11 and VMS and the file system used by Tenex and TOPS-20 have provisions for a version number as part of a file’s fully qualified name. If a file was opened without reference to a version number, the most recent version was used. When a file was created