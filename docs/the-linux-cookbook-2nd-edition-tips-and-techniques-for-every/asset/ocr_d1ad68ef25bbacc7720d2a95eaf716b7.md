# Appendix C. Setting Up Your Home Directory

Your home directory is the place where you keep your own files. Good organizational skills and some foresight will help keep your “home” in order. This appendix is all about giving hints for organizing your home directory.

You’ll find that the home directory as outlined here mirrors, in many ways, the /usr/local directory tree, which itself somewhat mirrors the system root directory, /; this is no coincidence. The Linux directory tree structure is well-organized and lends itself to this purpose; I’ve found that the home directory, and directories for any particular project or “thing,” usually have some similar directories and files: bin, doc, etc, src, tmp, THANKS, passwd, and so on.

You can configure your home directory any way you like, and you can change it at any time, of course. There is no rule that says, “You must store this kind of file in a directory here,” “You must have an etc,” or anything like that. Here is what I do.

# C.1 Using a Directory for Personal Binaries

A directory for binaries is simply a directory where you store executable files. To make the shell recognize it, add this directory to your PATH variable, as defined in your ~/.bashrc file. The directory can have any name. I prefer sticking with the bin convention and putting it right in the home directory: ~/bin.

⇒ To make your own bin directory and add it to your path, do the following:

+   1. Use mkdir to make a bin directory in your home directory:
+      $ mkdir ~/bin [RET]

+   2. Use a text editor to edit your .bashrc, and change the path to include ~/bin (see Recipe 3.5.7 [Adding to Your Path], page 81). It is a quoted, comma-delimited list. For example:
+      PATH="/usr/local/bin:/usr/bin:/bin:/usr/bin/X11:/usr/games:~/bin:."

In your own bin, you can put scripts and tools of your own devising. They will be executable by you, but by no other users on the system. To make a file executable by all users, the superuser will have to put the file in /usr/local/bin, the system-wide local directory for binaries.

NOTES: The current shell won’t recognize any changes you make in your .bashrc; you’ll have to run it by hand the first time, or just exit and start a new shell.