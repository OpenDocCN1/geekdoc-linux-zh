# **To change file and directory permissions:**

+   1. Make sure that you are in your home directory.

+   2. Type `chmod go+x ~` and press **Enter** to allow access to your home directory. This command means “make your home directory (~) accessible (+x) to the group (g) and others (o).”

+   3. Type `chmod ugo+x ~/corp_db` and press **Enter** to allow access to the corp_db directory. This command means “make the corp_db directory accessible (+x) for the owner (u), group (g), and others (o).”

+   4. Type `chmod ugo+r ~/corp_db/corp_phones` and press **Enter** to set permissions so everyone can read the file. This command means “make the corp_phones file readable (+r) for the owner (u), group (g), and others (o).”

Note: From your home directory, you can create any subdirectory and set permissions for it. However, you cannot create subdirectories outside your home directory unless the system administrator makes a special provision.

You used the appropriate UNIX commands to create new directories to store files and set up a central directory for all users, and then you transferred files from other directories to the central directory. Finally, you changed file permissions so other users can access the directories and files you created.

# # S U M M A R Y

+   - In UNIX, a file is the basic component for data storage. UNIX considers everything to be a file, even attached devices such as the monitor, keyboard, and printer.

+   - A file system is the UNIX system’s way of organizing files on mass storage devices such as hard and floppy disks. Files are stored on a file system, which is a hierarchical structure like a tree where top-level directories contain other directories, which in turn contain other directories.

+   - Every file can be located by using a correct and unique pathname; that is, a listing of names of directories leading to a particular file.

+   - The standard tree structure starts with the root ( / ) directory, which serves as the foundation for a nested group of other directories and subdirectories.

+   - The section of the disk that holds a file system is called a partition. One disk may have many partitions, each separated from the others so that it remains unaffected by external disturbances such as structural file problems associated with another partition.

+   - The UNIX file system is designed to allow access to multiple partitions once they are mounted in the tree structure.