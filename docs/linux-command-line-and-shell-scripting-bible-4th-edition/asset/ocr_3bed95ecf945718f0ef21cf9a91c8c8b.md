|              |       | compression algorithm and Huffman coding |
| compress | . z | Original Unix file compression utility; starting to fade away into obscurity |
| gzip | . gz | The GNU Project’s compression utility; uses Lempel-Ziv-Welch coding |
| xz | . xz | A general-purpose compression utility gaining in popularity |
| zip | . zip | The Unix version of the PKZIP program for Windows |

The compress file compression utility is not often found on Linux systems. If you download a file with a . z extension, you can usually install the compress package (called ncompress in many Linux distributions) using the software installation methods discussed in Chapter 9, “Installing Software,” and then uncompress the file with the uncompress command. The gzip utility is the most popular compression tool used in Linux.

The gzip package is a creation of the GNU Project in their attempt to create a free version of the original Unix compress utility. This package includes these files:

+   • gzip for compressing files
+   
+   • gzcat for displaying the contents of compressed text files
+   
+   • gunzip for uncompressing files

These utilities work the same way as the bzip2 utilities:

```
$ gzip myprog
$ ls -1 my* 
-rwxrwxr-x 1 rich rich 2197 2007-09-13 11:29 myprog.gz
$ 
```

The gzip command compresses the file you specify on the command line. You can also specify more than one filename or even use wildcard characters to compress multiple files at once:

```
$ gzip my* 
$ ls -1 my* 
-rwxr-r-r--     1 rich        rich            103 Sep   6 13:43 
```