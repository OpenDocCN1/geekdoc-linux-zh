See uncompress for details on how to uncompress the compressed file.

# gunzip

Syntax: gunzip [-v] file(s)

To decompress files to their original form, use the gunzip command. gunzip attempts to decompress files ending with the following extensions: .gz, -gz, .z, -z, _z, .Z, or tgz.

The -v option displays a verbose output when decompressing a file.

```
gunzip -v README.txt.gz
README.txt.gz:          65.0%-replaced with README.txt
```

See gzip for details on how to compress a file that can be uncompressed by gunzip.

# gzip

Syntax: gzip [-rv9] file(s)

The gzip command is a compression program that's known for having one of the best compression ratios, but at a price: gzip can be considerably slow. Files compressed with gzip are replaced by files with a .gz extension and can be unzipped with the gunzip command (which is discussed in the previous section).

The -9 option yields the best compression, but sacrifices speed. The -v option is the verbose option: the size, total, and compression ratios are listed for each file. Also, the -r option recursively traverses each directory, compressing files along the way.

```
ls -aIF README.txt
-rw-r--r--  1 root     root          16213 Oct 14 13:55 README.txt
```

```
gzip -9v README.txt
README.txt:          65.0%-replaced with README.txt.gz
```

```
ls -aIF README.txt.gz
-rw-r--r--  1 root     root           5691 Oct 14 13:55 README.txt.gz
```

See gunzip for details on how to uncompress a gzipped file.