### EXEMPLES

**This Command**

**Does the Following**

bunzip2 kdeapp.tar.bz2

Decompresses the specified file.

bunzip2 -keep kdeapp.tar.bz2

Decompresses the specified file without deleting the input file.

# # bzip2

**bzip2 [ option ] filename**

Compresses the specified filename using a sophisticated algorithm that is up to 30 percent faster than that used by **gzip**. For *filename*, specify the name of the file or files to be archived. You can use a shell pattern (see the section “Shell Patterns” in *Chapter 4*) or a space-separated list of files. By default, **bzip2** does not overwrite existing output files. (Use the `--force` option to override this setting.) However, the program deletes input files by default (use `--keep` to override this setting) and writes the compressed file with the `.bz2` extension.

Use **bunzip2** to decompress files compressed with **bzip2**. Use **bzip2recover** to recover data from damaged **bzip2** files.

### OPTIONS

**Use This Option**

**To Do This**

--

Treat all subsequent arguments as filenames, which enables you to work with files beginning with a dash.

-1, -2, -3, -4, -6, -7, -8, -9

Set the block size to the specified number times 100,000 bytes. The default is 100,000 bytes. If you have sufficient RAM, try using -2 or -3 to improve **bzip2**’s performance.