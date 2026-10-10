# **The tar Command (Archive)**

| Option | Action | Comment |
| --- | --- | --- |
| ▼ -x | Extracts files from an |  |
| ▼ --extract | archive. |  |
| ▼ --get |  |  |
| ▼ -z | Compress or unco- | --compress can also be |
| ▼ -Z | presses using gzip. | used to compress. |

# ### Compressing and decompressing Files With the gzip Command

The gzip command is one of the two Linux tools for compressing and decompressing files. The other is bzip2. The bzip2 command can compress files more, but gzip is more common, and can sometimes read zipped files, or compressed files created with the obsolete tool compress.

A file compressed using gzip has a .gz extension.

Type: **gzip OPTIONS FILES**.

Separate file names with a space.

The gzip command has several related utilities:

+   * ▼ zcat: Displays files in a gzip archive.
+   * ▼ zcmp: Compares files in a gzip archive.
+   * ▼ zdiff: Compares files in a gzip archive.
+   * ▼ zgrep, zegrep, zlgrep: Search for text patterns in files in a gzip archive.
+   * ▼ gunzip: decompresses files. However, gzip -d also decompresses.