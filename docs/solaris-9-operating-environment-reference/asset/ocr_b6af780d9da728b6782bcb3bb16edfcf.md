# gznew — Recompress .Z Files to .gz Files

# Synopsis

/bin/gznew [-ftv9PK] [name.Z...]

# Description

Use the gznew command, new in the Solaris 8 Operating Environment, to recompress files from .Z (compress) format to .gz (gzip) format. To recompress a file already in gzip format, rename the file to a .z extension and then apply gznew.

# Options

+   -g Use the slowest compression method (optimal compression).
-f Force recompression from .Z to .gz format even if a .gz file already exists.
-K Keep a .z file when it is smaller than the .gz file.
-P Use pipes for the conversion to reduce disk space use.
-t Test the new files before deleting originals.
-v Display the name and percentage reduction for each file compressed.

# Attributes

See attributes(5) for descriptions of the following attributes

| Attribute Type | Attribute Value |
| Availability | SUNWgzip |

# See Also

compress(1), gzdiff(1), gzexe(1), gzforce(1), gzipgrep(1), gzip(1), gzmore(1)

# Bugs

gznew does not maintain the timestamp with the -P option if cpmod(1) is not available and touch(1) does not support the -r option.