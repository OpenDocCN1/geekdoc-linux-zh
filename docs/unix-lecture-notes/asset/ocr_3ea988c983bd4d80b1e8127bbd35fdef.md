# Appendix A

# A.1 Useful Command-Line Options for ls

Some of the most useful command-line options for ls are listed below, with brief descriptions.

| Option | Description |
| --- | --- |
| -a | show dot-files (i.e. hidden files) |
| -l | display a long listing, with file type, permissions, number of links, owner, group, size in bytes, time of last modification |
| -lu | same as ls -l, except uses the last time the file was read instead of modified. |
| -s | show the file size in blocks |
| -t | sort the files by timestamp specified (u for access, modification by default) |
| -F | show file types |
| -i | show the i-number of the file |
| -d | if ls has a directory argument, show the attributes of the directory, instead of its contents |
| -R | recursively descend any directories or their subdirectories, applying any other options listed |

As you can see, several of these options can be extremely useful when searching for things in the file system. A "dot-file" is not a file filled with dots. It is a file whose name begins with a dot, such as ".bashrc" or ".login" or ".evolution". You read the first as "dot-bash-R-C", and the second as "dot-login". Dot-files are thought of as hidden files because the plain ls command does not display files whose names begin with a dot, and ls is the only command to view the content of a directory. Even in desktop environments, the default settings of a browser like Nautilus will hide these files. In your home directory, if you type "ls -a" you will see all of the files and directories whose names begin with a dot. In this list you will see "." and "..". Recall that these refer to the directory itself and its parent. Note that unlike Windows, the UNIX kernel has no concept of a hidden file.

# A.1.1 Bit Masks

Suppose we want to extract the value of bit 8 of some 16-bit number named flags. If we perform a bitwise AND of flags and the binary number that has 0's everywhere except in bit 8, called mask8 here, as illustrated:

| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | mask8 |
| b15 | b14 | b13 | b12 | b11 | b10 | b9 | b8 | b7 | b6 | b5 | b4 | b3 | b2 | b1 | b0 | flags |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | b8 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | mask8 & flags |