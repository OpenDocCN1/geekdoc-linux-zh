```
maillog.txt: 92.3% -- replaced with maillog.txt.gz
proposal.doc: 79.9% -- replaced with proposal.doc.gz
rowing-w-jasmine2.jpg: 0.2% -- replaced with rowing-w-jasmine2.jpg.gz
```

It did an outstanding job compressing the maillog.txt file: Compared to the 3.6MB average for compress, gzip has shrunk it down to 2.9MB. However, one annoying characteristic of gzip is that it compresses just about everything, even if the savings are pointless (the JPEG image has been compressed 0.2%, and the original file that was 522Kb has been replaced with its gzipped version that's 521Kb.

Here's how our four files compressed with the regular gzip invocation:

```
-rw-r--r-- 1 taylor coders 2992332 Jan 21 16:08 maillog.txt.gz
-rw-r--r-- 1 taylor coders 4197440 Jan 21 12:41 Nice Work.mp3.gz
-rw-r--r-- 1 taylor coders 26159 Jan 21 12:42 proposal.doc.gz
-rw-r--r-- 1 taylor coders 521565 Jan 21 12:43 rowing-w-jasmine2.jpg.gz
```

To uncompress them is a simple matter of invoking gunzip

```
$ gunzip *.gz
```

and compressing them with a higher requested compression ratio (the -9 flag):

```
$ gzip -v9 Nice* maillog* prop* rowing*
```

```
Nice Work.mp3: 2.4% -- replaced with Nice Work.mp3.gz
maillog.txt: 93.3% -- replaced with maillog.txt.gz
proposal.doc: 80.1% -- replaced with proposal.doc.gz
rowing-w-jasmine2.jpg: 0.2% -- replaced with rowing-w-jasmine2.jpg.gz
```

The result files are just a tiny bit smaller:

```
-rw-r--r-- 1 taylor coders 2604313 Jan 21 16:08 maillog.txt.gz
-rw-r--r-- 1 taylor coders 4197118 Jan 21 12:41 Nice Work.mp3.gz
-rw-r--r-- 1 taylor coders 25850 Jan 21 12:42 proposal.doc.gz
-rw-r--r-- 1 taylor coders 521565 Jan 21 12:43 rowing-w-jasmine2.jpg.gz
```

Better, but probably not enough to worry about whether you remember to use the -9 flag or not!

3. One great capability of gzip is its ability to recursively compress every file in the current directory and any subdirectory from a given point:
$ cd -testdud e
$ gzip -rv9 *
adduser.sh: 46.3% -- replaced with adduser.sh.gz
browse.sh: 57.1% -- replaced with browse.sh.gz
checkhomes.sh: 50.4% -- replaced with checkhomes.sh.gz
checkpwp.sh: 38.8% -- replaced with checkpwp.sh.gz
delete.sh: 43.7% -- replaced with delete.sh.gz