5. It turns out that in the world of Red Hat Linux, there are a number of utilities that can work directly with compressed files, as summarized in the following listing:

```
zcat [compress]      (1)  - compress and expand data (version 4.1)
zcat [gzip]          (1)  - compress or expand files
zcat [uncompress]    (1)  - compress and expand data (version 4.1)
zcmp [zdiff]         (1)  - compare compressed files
zdiff                (1)  - compare compressed files
zgrep                (1)  - search possibly compressed files for expression
zless                (1)  - file perusal filter for viewing compressed text
zlib                 (3)  - compression/decompression library
zmore                (1)  - file perusal filter for viewing compressed text
znew                 (1)  - recompress .Z files to .gz files
```

6. It's also fun and illustrative of the subtle differences between Unix flavors to see how the same command compressing the same original files has different results on different Unix platforms.

```
Red Hat Linux 7.2:
$ compress -v Nice* mailog* prop* rowing*
Nice Work It.mp3: No compression ... Nice Work.mp3 unchanged
mailog.txt: ... replaced with mailog.txt.Z Compression: 90.66%
proposal.doc: ... replaced with proposal.doc.Z Compression: 62.31%
rowing-w-jasmine2.jpg: No compression ... rowing-w-jasmine2.jpg unchanged
```

```
Solaris 8:
$ compress -v Nice* mailog* prop* rowing*
Nice Work.mp3: Compression: -29.87% ... file unchanged
mailog.txt: Compression: 90.80% ... replaced with mailog.txt.Z
proposal.doc: Compression: 62.31% ... replaced with proposal.doc.Z
rowing-w-jasmine2.jpg: Compression: -30.28% ... file unchanged
```

```
Darwin/Mac OS X:
$ compress -v Nice* mailog* prop* rowing*
Nice Work.mp3: file would grow; left unmodified
mailog.txt.Z: 9% compression
proposal.doc.Z: 58% compression
rowing-w-jasmine2.jpg: file would grow; left unmodified
```

Amazingly, the resultant size of the mailog.txt file is different on each of the platforms, as summarized in Table 7.1.

Table 7.1 Variation in Compressed File Size
| Filename | Original Size | Linux | Solaris | Darwin |
|---|---|---|---|---|
| mailog.txt | 39,350,440 | 3,677,629 | 3,696,761 | 3,696,039 |

As you spend more time digging around on your Unix system, you'll inevitably find huge files that are rarely accessed. Perhaps an old development project saved in an