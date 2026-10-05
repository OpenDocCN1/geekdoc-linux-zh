# Deleting Files

The rm command deletes files in a text-mode shell. As you might expect, you pass the names of one or more files to this command:

```
$ rm outline.pdf outline.txt
```

This example deletes two files, outline.pdf and outline.txt. If you want to delete an entire directory tree, you can pass rm -r, -R, or --recursive with a directory name:

```
$ rm -r oldstuff/
```

The -i causes rm to prompt before deleting each file. This is a useful safety measure. If you use the -f (--force) to override this setting, if -i is configured as the default. Other options to rm exist; consult its man page to learn about them.

It's important to realize that rm does not implement any functionality like a file manager's "trash can." Once you delete a file with rm, it's gone, and you can't recover it except using low-level filesystem tools—a topic that's well beyond the scope of this book. You should be careful when using rm—and even more when using it with its -r option or as root!

# Using Wildcards

A wildcard is a symbol or set of symbols that stands for other characters. You can use wildcards to refer to files. (Using wildcards is sometimes called globbing). Three classes of wildcards are common in Linux:

+   ? A question mark (?) stands for a single character. For instance, b?? matches book, bald, buck, or any other four-character filename that begins with b and ends with k.

+   * An asterisk (*) matches any character or set of characters, including none. For instance, b*k matches book, bald, and buck (just as b?? does). b*k also matches bbk, bbb, and backtrack.

**Bracketed Values** enclosed in square brackets ([]) normally match any character in the set. For instance, b[ao][l0] matches bald and book but not. It's also possible to specify a range of values; for instance, b[a-z]ck matches back, buck, and other four-letter filenames of this form whose second character is a lowercase letter. This differs from b?ck—because Linux treats filenames in a case-sensitive way and because ? matches any character (not just letter), b[a-z] doesn't match b3ck, although b?ck matches both of these filenames.