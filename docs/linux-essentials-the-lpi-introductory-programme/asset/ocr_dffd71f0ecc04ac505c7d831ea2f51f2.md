# 11.3 Compressing Files with gzip

The most common compression program for Linux is `gzip` by Jean-loup Gailly and Mark Adler. It is used to compress single files (which, as mentioned earlier, may be archives containing many files).

The `gzip` program (short for “GNU *zip*”) was published in 1992 to avoid problems with the `compress` program, which was the standard compression tool on proprietary Unix versions. `compress` is based on the Lempel-Ziv–Welch algorithm (LZW), which used to be covered by US patent 4,558,302. This patent belonged to the Sperry (later Unisys) corporation and expired on 20 June 2003. On the other hand, `gzip` uses the DEFLATE method by Phil Katz [RFC1951], which is based on a non-patented precursor of LZW called LZW77 as well as the Huffman encoding scheme and is free of patent claims. Besides, it works better than LZW.

`gzip` can *decompress* files compressed using `compress`, because the Unisys patent only covered compression. You can recognise such files by the ".*z*" suffix of their names.

`gzip` is not to be confused with PKZIP and similar Windows programs with “ZIP” in their names. These programs can compress files and then archive them immediately; `gzip` only takes care of the compression and leaves the archiving to programs like `tar` or `cpio`.—`gzip` can unpack ZIP archives as long as the archive contains exactly one file which has been packed using the DEFLATE method.

`gzip` processes and replaces single files, appending the File*.gz* suffix to their names. This substitution happens independently of whether the resulting file is actually smaller than the original. If several files are to be compressed into a single archive, `tar` and `gzip` must be combined.

The most important options of `gzip` include:

+   * -c writes the compressed file to standard output, instead of replacing the original; the original remains unmodified
+   * -d uncompresses the file (alternatively: `gunzip` works like `gzip -d`)
+   * -l (“list”) displays important information about the compressed file, such as the file name, original and packed size
+   * -r (“recursive”) compresses files in subdirectories
+   * -5 (*suffix*) uses the specified suffix in place of `.gz`
+   * -v outputs the name and compression factor of every file
+   * -1 – -9 specifies a compression factor: -1 (or --fast) works most quickly but does not compress as thoroughly, while -9 (or --best) results in the best compression at a slower speed; the default setting is -6.

The following command compresses the letter.tex file, stores the compressed file as letter.tex.gz and deletes the original:

```
$ gzip letter.tex
```

The file can be unpacked using

```
$ gzip -d letter.tex
```

or