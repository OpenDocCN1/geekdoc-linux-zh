# Using Compression

In Linux, the gzip, bzip2, and x programs all compress individual files. For instance, you might compress a large graphics file like this:

```
$ x biggraphics.tiff
```

The result is a file with a name like the original but with a new filename extension to identify it as a compressed format. In this specific case, the result would be biggraphics.tiff.xz.

Most graphics programs won't read files compressed in this way. Thus to use a file that's compressed, you must uncompress it with a matching program. To uncompress the biggraphics.tiff.xz file compressed in the previous example, use this command:

```
$ un biggraphics.tiff.xz
```

Table 8.9 summarizes the compression programs, their matching uncompression programs, and the filename extensions they create.

TABLE 8.9 Compression and uncompression programs and filename extensions

| Compression program | Uncompression program | Filename extension |
| --- | --- | --- |
| gzip | gzip | .gz |
| bzip2 | bunzip2 | .bz2 |
| xz | unxz | .xz |

> As a general rule, gzip provides the least compression, and xz the most compressed. This is why the Linux kernel is known for compressed with xz.

The tar program provides explicit support for all three of compression standards, and tarballs often have their own unique filename extensions that indicate the compression used:

+   * .gz for tarballs compressed with gzip
* .tbz or .tb2 for tarballs compressed with bzip2
* .txz for tarballs compressed with xz

> Sometimes two extensions are used on a tarball archive file, resulting in a file such as my-work.tar.bz2.

When you use compression to create a tarball (using the z, j, or Option to tar), the compression program works on the entire tarball with all of its files rather than individually compressing each file within the tar. This can improve the compression ratio compared to compressing individual files and when bundling them together. However, it makes harder to extract data from a file if it becomes damaged.

> Typically, plaintext files compress extremely well, binary program files compress moderately well, and precompressed data (such as video file formats) poorly or even expand in size when compressed.

* With