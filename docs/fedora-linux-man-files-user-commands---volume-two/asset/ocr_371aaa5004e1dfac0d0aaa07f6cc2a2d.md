# EXAMPLES

To update and refresh only the files already checked out

```
$ git checkout-index -n -f -a && git update-index --ignore-missing --refresh
```

Using git checkout-index to “export an entire tree”

The prefix ability basically makes it trivial to use git checkout-index as an “export as tree” function. Just read the desired tree into the index, and do:

```
$ git checkout-index --prefix=git-export-dir/ -a
```

git checkout-index will “export” the index into the specified directory.

The final “/” is important. The exported name is literally just prefixed with the specified string. Contrast this with the following example.

Export files with a prefix

```
$ git checkout-index --prefix=.merged- Makefile
```

This will check out the currently cached copy of Makefile into the file .merged-Makefile.