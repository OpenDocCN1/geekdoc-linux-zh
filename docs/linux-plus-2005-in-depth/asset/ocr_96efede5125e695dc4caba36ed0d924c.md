the compress utility and save the compressed information to a file called file.Z, you can execute the following command:

```
```
[root@server1 root]# compress -v >file.Z
Compression: 21.35%
[root@server1 root]# _
```
```

Following this, you can display the contents of file.Z using the zcat command, or decompress it using the uncompress command, as shown in the following output:

```
```
[root@server1 root]# zcat file.Z
root pts/1 Jul 20 19:22 (3.0.0.2)
root tty5 Jul 15 19:03
root pts/1 Jul 17 19:58
[root@server1 root]# uncompress -v file.Z
file.Z: -- replaced with file
[root@server1 root]# _
```
```

Table 12-1 provides a summary of options commonly used with the compress utility.

**Table 12-1 Common options used with the compress utility**
| Option | Description |
| :--- | :--- |
| -c | When used with the uncompress command, it displays the contents of the compress file to Standard Output (same function as the zcat command). |
| -f | When used with the compress command, it can be used to compress symbolic links. When used with the uncompress command, it overwrites any existing files without prompting the user. |
| -r | Specifies to compress or decompress all files recursively within a specified directory. |
| -v | Displays verbose output (compression ratio and filenames) during compression and decompression. |


# The gzip utility

The GNU zip (gzip) utility uses a Lempel-Ziv compression algorithm (LZ77) that varies slightly from the one used by the compress utility. Typically, this algorithm yields better compression than the one used by compress; the average compression ratio for gzip is 60–70%.

Like the compress utility, symbolic links are not compressed by the gzip utility unless the -f option is given, and the -r option can be used to compress all files in a certain directory. In addition, the ownership, modification, and access times of compressed files are preserved by default, and the -v option to the gzip command can be used to display the compression ratio and filename. However, gzip uses the .gz filename extension by default.