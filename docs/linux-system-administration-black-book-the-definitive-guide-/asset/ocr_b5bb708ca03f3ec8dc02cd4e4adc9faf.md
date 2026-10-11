| Table 3.8 Popular flags used with the fsck command. | | | | | Flag | Purpose | -r | Checks with the person running the command before making repairs, instead of making them automatically. -t | Signals that the person running the command will specify the only file system type to check. -A | Checks every file system defined in /etc/fstab. Best used in conjunction with -t to ensure that only ext2 file systems are checked. -V | Runs in verbose mode. |

# Backing Up And Restoring File System Structure

Sometimes it is worthwhile to back up the structure of your file system separate from the file system itself. This information is immensely useful to have if you accidentally alter permissions or ownerships in important sections of the file system, or a misguided program does it for you. Trying to backtrack and fix things without a roadmap is not pleasant.

# Backing Up File System Structure

Make a backup of the file system structure in the following manner:

+   1.  Because you want to include the entire file system, type “cd /” to go to the root of your file system.
+   2.  Type “ls -IR > listing” to save the file system structure to the file “listing”. 
+   3.  If desirable, compress the listing by typing “gzip listing”, which gives you a file called listing.gz.

TIP: This method is also how the large Linux FTP sites are able to offer a file containing the listing of their directories. They just begin the command from the top of the FTP file system, not from the machine’s file system.

Related solutions: | Found on page: | Creating Gzipped Files | 108 | Creating Z Compressed Files | 108 | Opening Or Creating Tarballs | 110

# Restoring File System Structure

Restoring the structure of your file system after a “glitch” is not as easy as just typing a single command. However, there is a straightforward process to follow:

+   1.  Locate the file containing your file system listing, for example, /listing.gz.