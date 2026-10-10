# **Warning**

cp also has a `-r` option that does almost the same thing as `-R;` do not use it. The `-R` option copies special files, such as device files, correctly; the `-r` option assumes that all non-directory files are normal files and tries to read them as normal files. This could cause serious problems if the hierarchy you are copying contains device files.

+   *   `-p` Preserves the original files' owner, group, permissions, and modification and access times. (The owner and group cant only be preserved if you run `cp` as root.)
+   *   `-d` Does not follow symbolic links. Normally, `cp` treats symbolic links as normal files and copies the files to which they point. The `-d` option causes it to copy only the link itself. This option is not standardized by POSIX; it is available only with GNU `cp`.
+   *   `-a` Preserves as much of the original structure and attributes of the original tree as possible. The `-a` option is equivalent to `-dpR`.

cp has many more options for such things as making symbolic links instead of actual copies and making versioned backups of destination files. Consult cp (1) for details.

# ## Finding Files: `find`

The `find` command is one of the most powerful and useful commands in UNIX. It’s also fairly hard to master.

Essentially, `find` does the following:

+   *   Starts from an initial path (or set of paths)
+   *   Finds files that meet certain criteria
+   *   Does something with the filenames

Thus, you supply three pieces of information to `find`:

+   *   The starting path
+   *   The criteria for files you’re interested in
+   *   The action to be taken when an interesting file is found

Let’s look at an example before diving into the syntax:

```
$ `find /usr/doc -name '*mail*' -print`
`/usr/doc/fetchmail-4.7.7`
`/usr/doc/fetchmail-4.7.7/fetchmail-FAQ.html`
`...`
```