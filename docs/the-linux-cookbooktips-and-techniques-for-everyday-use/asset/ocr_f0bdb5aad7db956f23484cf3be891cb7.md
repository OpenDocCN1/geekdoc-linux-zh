checked in, ci prompts for text to include in the file's revision log (see section Viewing a File's Revision Log). Log messages may contain more than one line of text; type a period ( '.' ) on a line by itself to end the entry.

For example, suppose the file `novel` contains this text:

```
This is a tale about many things, including a long voyage across
America.
```

+   - To check in the file `novel` with RCS, type:

```
$ ci novel RET
novel,v  60:-- novel
enter description, terminated with single '.' or end of file:
NOTE: This is NOT the log message!
62;62; The Great American Novel. RET
62;62; . RET
$
```

This command deposits the file in an RCS repository file called `novel,v`, and the original file, `novel`, is removed. To edit or access the file again, you must check out a revision of the file from RCS with which to work (see section Checking Out a File Revision).

Whenever you have a new revision that you want to save, use ci as before to check in the file. This begins the process all over again.

For example, suppose you have checked out the first revision of `novel` and changed the file so that it now looks like this:

```
This is a very long tale about a great many things, including my long
voyage across America, and back home again.
```

+   - To deposit this revision in RCS, type:

```
$ ci novel RET
novel,v  60:-- novel
new revision: 1.2; previous revision: 1.1
enter log message, terminated with single '.' or end of file:
62;62; Second draft. RET
62;62; . RET
$
```

If you create a subdirectory called `RCS` (in all uppercase letters) in the current directory, RCS recognizes this specially named directory instead of the current directory as the place to store the `,v` revision files. This helps reduce clutter in the directory you are working in.

If the file you are depositing is a text file, you can have RCS insert a line of text, every time the file is