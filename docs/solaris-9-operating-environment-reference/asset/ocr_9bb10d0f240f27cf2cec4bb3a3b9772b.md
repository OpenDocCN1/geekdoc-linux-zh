# gzforce — Force a .gz Extension on all gzip Files

# Synopsis

/bin/gzforce [name...]

# Description

Use the gzforce command, new in the Solaris 8 Operating Environment, to force a .gz extension on all files so that gzip does not compress them twice. This command can be useful for files with names truncated after a file transfer. On systems with a 14-character limitation on filename, the original name is truncated to make room for the .gz suffix. For example, 12345678901234 is renamed to 1234567891.gz. A file name as foo is left intact.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
| Availability | SUNgzip |

# See Also

gzdiff(1), gzexe(1), gzgrep(1), gzip(1), gzmore(1), gznew(1)

# gzip, gunzip, gzcat — Compress or Expand Files

# Synopsis

/bin/gzip [-acdfhlLnNqrtvV#] [-S suffix] [name...]
/bin/gunzip [-acdfhlLnNqrtvV] [-S suffix] [name...]
/bin/gzcat [-fhlV] [name...]

# Description

Use the gzip command, new in the Solaris 8 Operating Environment, to reduce the size of the named files with Lempel-Ziv coding (LZ77).

> Note — gzip is available in the SUNgzip package.

When possible, each file is replaced by one with the extension .gz, keeping the same ownership modes, access, and modification times. For VMS, the default extension is -gz. For MS-DOS/OS FAT, Windows NT FAT, and Atari, the default extension is z. When you specify no file or if a file is name -, the standard input is compressed to the standard output, gzip tries to compress regular files. It ignores symbolic links.
If the compressed file name is too long for the file system, gzip tries to truncate it. gzip truncates the parts of the name longer than 3 characters. A part is delimited by dots. If the name consists of same parts only, the longest parts are truncated. For example, if file names are limited to 14 characters, mdos.exe is