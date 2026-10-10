# The gzip Command (Compress)

| Option | Action | Comment |
|:-------|:-------|:--------|
| ▼ -n<br>▼ --no-name | Discards original name and time stamp. | This is the default setting for decompressing. |
| -number | Sets the speed and amount of compression on a scale of 1 to 9. | 1 is the fastest, 9 the most compressed.<br>The default setting is 6. |
| ▼ -r<br>▼ --recursive | Includes sub-directories and their contents. | |

# Compressing and decompressing With the bzip2 Command

The bzip2 command is one of two tools for compressing and decompressing files. The other is gzip. The gzip command is more common, but bzip2's compression is 10 to 20 percent greater, depending on the file.

Compressed files made with bzip2 have a .bz2 extension.

Type: bzip2 OPTIONS FILES.

Separate each name with a space.

The bzip2 command has three related utilities: