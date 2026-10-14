When you're finished with a tape, you can use mt offline to rewind the tape, take it offline, and eject it (if possible).

Relevant man pages: mt (1)

# tar

We've already demonstrated the three basic main modes of tar: for creating, extracting, and testing archives. To make tar work, you must put it into a mode. You may specify the modes and modifying options together; in the examples above, we've used the v option twice (vv) to get an extra-verbose listing of the files involved. The three mode options mentioned so far are c for create, t for test, and x for extract. Important modifying options include these:

+   - **f** The file name of the device or archive follows. When you use this option, the next argument must be the file name. Use a hyphen (-) to indicate standard output, as in this example:
+     `$ zcat foo.tar.gz | tar tvf -`

+   - **v** Be verbose; show more information about the files in the archive. If you give this option twice, you'll get a listing similar to that of ls -l.

+   - **p** Preserve permissions when extracting, overriding any permissions mask (set with umask).

+   - **z** Use GNU zip compression. New archives (when tar is used with the c option) run through gzip -c first; extractions and tests (tar's x and t options) use gzip -dc.

> NOTE There is nothing special about a tar archive. You can put any file on the tape; for example, if you wanted to put /etc/services at the current place on the tape, you'd run:

```
# dd if=/etc/services of=$TAPE
```

Relevant man page: tar (1)

# dd

One of the hidden treasures of Unix is a program called dd. It stands for convert and copy. dd differs from cat in that dd knows a bunch of obscure data coding formats as well as tricks on buffering and regulation of I/O flow. If you need to use your tape drive, disk, or other block device for some task that's a little out of the ordinary, dd is the first command you should look at, because it knows how to deal with the fixed-length chunks of data that block devices want. dd also works on plain files, but the block size specification is irrelevant in this case (other than for a few special tricks).