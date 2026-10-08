# Nomadic Machines

When using filesync to keep files synchronized between nomadic machines and a server, store the packing files and baseline files on the nomadic machines, not the server. if you are logged into your notebook, the HOME environment variable does not normally point to a directory in your notebook, you can use the FILESYNC environment to specify an alternate location for the packing files and baseline files.

Each nomadic machine carries its own packing files and baseline rules. Incorrect file synchronization can result if a server carries a baseline file and multiple nomadic machines attempt to reconcile the server's baseline file. In this case, a nomadic machine could be using a baseline file that does not accurately describe the state of its files, which might result in incorrect reconciliations.

To safeguard the dangers associated with a single baseline file being shared by more than two machines, filesync adds a default rule to each new packing rules file. This default rule prevents the packing rules and baseline files from being copied.

# Options

+   - Force the checking of Access Control Lists (ACLs), and try to make them agree for all new and changed files. If it is not possible to set the ACL for a particular file, filesync stops ACL synchronization for that file.

+   - Some systems do not support ACLs. It is not possible to synchronize ACLs between file systems that support ACLs and those that do not; trying to do so results in numerous error messages.

+   - Specify the directory on the destination system into which filename is to be copied. Use with the -source-direction and the filename operand. Specify -s.

+   - Flag all differences. It may not be possible to resolve all conflicts involving modes and ownership (unless filesync is being run with root privileges). If you change the ownership or protections on a file, filesync normally ignores conflicts in ownership and protection. If you specify the -e (everything must agree) flag, filesync flags these as differences.

+   - Specify how to resolve conflicting changes. If a file has been changed on both systems and you specify the -f option, retain the changes made on the favored system and discard the changes made on the unfavorable system.

+   - -f src to favor the source system file. Specify -f dst to favor the destination system file. Specify -f old to favor the older version of the file. Specify -f new to favor the newer version of the file.

+   - You can combine the -f and -o options if both specify the same preference (src or dst). If -f and -o conflict, ignore the -f option.