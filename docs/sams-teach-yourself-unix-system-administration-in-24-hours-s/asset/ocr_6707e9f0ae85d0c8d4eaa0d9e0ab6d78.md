can include the special name - to compress standard input.
If zipfile and list are omitted, zip compresses stdin to stdout.

-f freshen: only changed files    -u update: only changed or new files
-d delete entries in zipfile      -m move into zipfile (delete files)
-r recurse into directories       -j junk (don't record) directory names
-0 store only                     -1 convert LF to CR LF (-11 CR LF to LF)
-1 compress faster                -9 compress better
-q quiet operation                -v verbose operation/print version info
-c add one-line comments          -z add zipfile comment
-o read names from stdin          -o make zipfile as old as latest entry
-x exclude the following names    -i include only the following names
-F fix zipfile (-FF try harder)   -D do not add directory entries
-A adjust self-extracting exe     -J junk zipfile prefix (unzipspx)
-T test zipfile integrity         -X eXclude extra file attributes
-y store symbolic links as the link instead of the referenced file
-R PKZIP recursion (see manual)   -n don't compress these suffixes
-e encrypt

To build a PKZIP-compatible archive, you want to ensure that you use the following flags: -r causes the program to recurse into subdirectories and include that content too, -9 requests the best possible compression, and -v offers verbose output:

```
$ zip -r -9 -v testdude.zip *
  adding: adduser.sh (in=1113) (out=597) (deflated 46%)
  adding: browse.sh (in=739) (out=317) (deflated 57%)
  adding: checkhomes.sh (in=537) (out=266) (deflated 50%)
  adding: checkpw.sh (in=756) (out=462) (deflated 39%)
  adding: delete.sh (in=693) (out=390) (deflated 44%)
  adding: DEMO/ (in=0) (out=0) (stored 0%)
  adding: DEMO/testfile (in=0) (out=0) (stored 0%)
  adding: DEMO/Src/ (in=0) (out=0) (stored 0%)
  adding: DEMO/Src/cribbage.c (in=26150) (out=8081) (deflated 69%)
  adding: DEMO/snapshot.sh (in=263) (out=187) (deflated 29%)
  adding: DEMO/sourcefiles.cpio... (in=153600) (out=41688) (deflated 73%)
  adding: DEMO/testdir/ (in=0) (out=0) (stored 0%)
  adding: diskhogs.sh (in=373) (out=234) (deflated 37%)
  adding: getmodemdriver.sh (in=605) (out=381) (deflated 37%)
  adding: getstocks.sh (in=569) (out=346) (deflated 39%)
  adding: gettermssheet.sh (in=593) (out=373) (deflated 37%)
  adding: rowing-w-jasmine2.jpg...... (in=522970) (out=521525) (deflated 0%)
  adding: suspend.sh (in=1290) (out=679) (deflated 47%)
  total bytes:710251, compressed=575526 -> 19% savings
```

Neatly done, and the file testdude.zip is now ready to e-mail to the user. Notice that the compressed value shown on the last line is in fact the size of the resultant archive file: 575,526 bytes.