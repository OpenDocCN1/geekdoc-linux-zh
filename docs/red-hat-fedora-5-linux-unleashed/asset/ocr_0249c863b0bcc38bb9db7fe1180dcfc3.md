vice versa. There doesn't seem to be any hard and fast rule about this, and most advice is to accept the default block size of 1024KB unless you want to spend some time running benchmarks.

# The tune2fs Command

With tune2fs, you can adjust the tunable file system parameters on an ext2 or ext3 file system. A few performance-related items of note are as follows:

+   To disable file system checking, the -c 0 option sets the maximum mount count to zero.
+   
+   The interval between forced checks can be adjusted with the -I option.
+   
+   The -m option will set the reserved blocks percentage with a lower value, freeing more space at the expense of fsck having less space to write any recovered files.
+   
+   Decrease the number of superblocks to save space with the -0 sparse_super option. (Modern file systems use this by default.) Always run e2fsck after you change this value.
+   
+   More space can be freed with the -r option that sets the number of reserved (for root) blocks.

Note that most of these uses of tune2fs free up space on the drive at the expense of the capability of fsck to recover data. Unless you really need the space and can deal with the consequences, just accept the defaults; large drives are now relatively inexpensive.

# The e2fsck Command

This utility checks an ext2/ext3 tile system. Some useful arguments taken from man e2fsck are as follows:

+   -c—Checks for bad blocks and then marks them as bad.
+   -f—Forces checking on a clean file system.
+   -v—Verbose mode.

# The badblocks Command

Although not a performance tuning program per se, the badblocks utility checks an (preferably) unmounted partition for bad blocks. It is not recommended that you run this command by itself, but rather allow it to be called by fsck. It should be used directly only if you specify the block size accurately—don't guess or assume anything.

The options available for badblocks are detailed in the man page. They allow for very low-level manipulation of the file system that is useful for data recovery by file system experts or for file system hacking, but is beyond the scope of this chapter and the average user.

# Disabling File Access Time

Whenever Linux reads a file, it changes the last access time—known as the atime. This is also true for your web server: If you are getting hit by 50 requests a second, your hard disk will be updating the atime 50 times a second. Do you really need to know the last