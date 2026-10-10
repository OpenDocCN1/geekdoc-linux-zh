# DESCRIPTION

Display file or file system status.

Mandatory arguments to long options are mandatory for short options too.

+   **-L**, **—dereference**
+   	follow links

+   **-f**, **—file-system**
+   	display file system status instead of file status

+   **-c** **—format=***FORMAT*
+   	use the specified FORMAT instead of the default; output a newline after each use of FORMAT

+   **—printf=***FORMAT*
+   	like **—format**, but interpret backslash escapes, and do not output a mandatory trailing newline; if you want a newline, include \n in FORMAT

+   **-t**, **—terse**
+   	print the information in terse form

+   **—help**
+   	display this help and exit

+   **—version**
+   	output version information and exit

The valid format sequences for files (without **—file-system**):

+   %a
+   	access rights in octal

+   %A
+   	access rights in human readable form

+   %b
+   	nuer of blocks allocated (see %B)

+   %B
+   	the size in bytes of each block reported by %b

+   %C
+   	SELinux security context string

+   %d
+   	device nuer in decimal

+   %D
+   	device nuer in hex

+   %f
+   	raw mode in hex

+   %F
+   	file type

+   %g
+   	group ID of owner