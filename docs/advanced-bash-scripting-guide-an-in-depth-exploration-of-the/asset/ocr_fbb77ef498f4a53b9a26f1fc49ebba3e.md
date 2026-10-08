# Chapter 20. I/O Redirection

Are are three default files [104] stdin (the keyboard), stdout (the screen), and stderr (error messages output to the screen). These, and any other files, can be redirected. Redirection means capturing output from a file, command, program, script, or even code block within a script (Example 3-1 and Example 3-2) and sending it as input to another file, command, program, or script.

Each file gets assigned a file descriptor. [105] The file descriptors for stdin, stdout, and stderr are 0, 1, and 2, respectively. For opening additional files, remaining descriptors are 3 to 9. It is sometimes useful to assign one of these additional file descriptors to stdin, stdout, or stderr as a temporary duplicate link. [106] This simplifies redirection to normal after complex redirection and reshuffling (Example 20-1).

```
COMMAND_OUTPUT =
# Redirect stdout to a file.
# Creates the file if not present, otherwise overwrites it.

ls -LR > dir-tree.list
# Creates a file containing a listing of the directory tree

: filename
# The truncates file "filename" to zero length.
# If file not present, creates zero-length file (same effect as 'touch').
# The serves as a dummy placeholder, producing no output.

filename
# The truncates file "filename" to zero length.
# If file not present, creates zero-length file (same effect as 'touch').
# (Same result as ">\ above, but this does not work with some shells.)

COMMAND_OUTPUT >>
# Redirect stdout to a file.
# Creates the file if not present, otherwise appends to it.

# Single-line redirection commands (affect only the line they are on):
#
1>filename
# Redirect stdout to file "filename.
1>>filename
# Redirect and append stdout to file "filename.
2>filename
# Redirect stderr to file "filename.
2>>filename
# Redirect and append stderr to file "filename.
&filename
# Redirect both stdout and stderr to file "filename.
# This operator is now functional, as of Bash 4, final result.

M>
# "M" is a file descriptor, which defaults to 1, if not explicitly set.
# "M" is a filename.
# File descriptor "M" is redirect to file "N."
M&N
# "M" is a file descriptor, which defaults to 1, if not set.
```