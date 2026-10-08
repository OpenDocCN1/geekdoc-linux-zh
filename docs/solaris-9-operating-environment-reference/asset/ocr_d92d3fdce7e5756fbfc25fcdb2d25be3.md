compressed to gzi.msd.exe. Names are not truncated on systems that have no limit
file-name length.

By default, gzip keeps the original file name and timestamp in the compressed file.
They are used when the file is decompressed with the -N option. This feature is useful
when the compressed file name was truncated or when the timestamp was not preserved
after a file transfer.

You can restore files to their original format with gzip -d, gunzip, or
gczat. If the original name was saved in the compressed file is not suitable for its file system,
a new, legal name is constructed from the original one.

gzip replaces each file on the command line with names ending with .gz, -gz,
-z, .Z, or begins with the correct magic number with an uncompressed file
without the original extension. gzip also recognizes the special extensions .tgz and
taz as shorthand for .tar.gz and .tar.Z. When compressing, gzip uses the .tgz
extension instead of decompressing a file with a .tar extension.

gunzip can decompress files by gzip, gunzip, compress, compress -H
or pack. Input format detection is automatic. With the first two formats, gunzip checks
a32-bit CRC. For pack, gunzip checks the uncompressed length. The standard
format was not designed to allow consistency checks; however, gunzip is
sometimes to detect a bad .z file. If you get an error whencompressing a .z file,
do not assume that the .z file is correct because the standard uncompress does
check its input and anyway generates garbage output. The SCO compress -H
format (lz compression) does not include a CRC but does allow some
consistency checks.

Files can be compressed by gzip only if they have a single member
compressed with the deflation method. This feature is intended to help conversion of
tar.zip to the tar.gz format. To extract files with several members, use unzip
tar instead of gunzip.

gzcat is identical to gunzip -c. (On some systems, zcat may be installed as gzcat
to preserve the original file line to compress.) gzcat uncompresses either a list of files on
t command line or its standard input and writes the uncompressed data to standard
out. gzcat uncompresses files that have the correct magic number regardless of
they have a .gz suffix.

gzip uses the Lempel-Ziv algorithm in gzip and ZIP. The amount of
compression depends on the size of the input and the distribution of common
substrings. Typically, text such as source code or English is reduced 60 to 70 percent.
Compression is much better than that achieved by LZW (as used by
compress), Huffman coding or Adaptive Huffman coding (compact).

Compression is always performed, even if the compressed file is slightly larger
then original. The work-expansion is a few bytes for the gzip file header plus 5 bytes
every 2KB blocks or an expansion ratio of 0.015 percent for large files. Note that the
actual number of disk blocks almost gzip preserves the mode,
ownership, and timestamps of files when compressing or decomposing.

# Options

+   -a ascii ASCII text mode. Convert end-of-lines with local conventions.
 option is supported only on some non-UNIX systems. For MS-DOS, CR
LF is converted to LF when compressing, and LF is converted to CR LF
 decompressing.