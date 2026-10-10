
(easily) have access to the complete set of bytes which normally goes into such a signature. If signing is required, create lightweight tags from within fast-import with reset, then create the annotated versions of those tags offline with the standard git tag process.

## reset

Creates (or recreates) the named branch, optionally starting from a specific revision. The reset command allows a frontend to issue a new from command for an existing branch, or to create a new branch from an existing commit without creating a new commit.

`'reset' SP <ref> LF ('from' SP <commit- ish> LF)? LF?`

For a detailed description of `<ref>` and `<commit- ish>` see above under commit and from.

The LF after the command is optional (it used to be required).

The reset command can also be used to create lightweight (non-annotated) tags. For example:

```
reset refs/tags/938 from :938
```

would create the lightweight tag refs/tags/938 referring to whatever commit mark :938 references.

## blob

Requests writing one file revision to the packfile. The revision is not connected to any commit; this connection must be formed in a subsequent commit command by referencing the blob through an assigned mark.

`'blob' LF mark? data`

The mark command is optional here as some frontends have chosen to generate the Git SHA-1 for the blob on their own, and feed that directly to commit. This is typically more work than it's worth however, as marks are inexpensive to store and easy to use.

## data

Supplies raw data (for use as blob/file content, commit messages, or annotated tag messages) to fast-import. Data can be supplied using an exact byte count or delimited with a terminating line. Real frontends intended for production-quality conversions should always use the exact byte count format, as it is more robust and performs better. The delimited format is intended primarily for testing fast-import.

Comment lines appearing within the `<raw>` part of data commands are always taken to be part of the body of the data and are therefore never ignored by fast-import. This makes it safe to import any file/message content whose lines might start with #.

### Exact byte count format

The frontend must specify the number of bytes of data.

`'data' SP <count> LF <raw> LF?`

where `<count>` is the exact number of bytes appearing within `<raw>`. The value of `<count>` is expressed as an ASCII decimal integer. The LF on either side of `<raw>` is not included in `<count>` and will not be included in the imported data.

The LF after `<raw>` is optional (it used to be required) but recommended. Always including it makes debugging a fast-import stream easier as the next command always starts in column 0 of the next line, even if `<raw>` did not end with an LF.

### Delimited format

A delimiter string is used to mark the end of the data. fast-import will compute the length by searching for the delimiter. This format is primarily useful for testing and is not recommended for real data.

```
'data' SP '<' <delim> LF <raw> LF <delim> LF LF?
```

where `<delim>` is the chosen delimiter string. The string `<delim>` must not appear on a line by itself within `<raw>`, as otherwise fast-import will think the data ends earlier than it really does. The LF immediately trailing `<raw>` is part of `<raw>`. This is one of the limitations of the delimited format, it is impossible to supply a data chunk which does not have an LF as its last byte.

The LF after `<delim>` LF is optional (it used to be required).

## checkpoint

Forces fast-import to close the current packfile, start a new one, and to save out all current branch refs, tags and marks.

```
'checkpoint' LF LF?
```

Note that fast-import automatically switches packfiles when the current packfile reaches --max-pack-size, or 4 GiB, whichever limit is smaller. During an automatic packfile switch fast-import does not update the branch refs, tags or marks.

As a checkpoint can require a significant amount of CPU time and disk I/O (to compute the overall pack SHA-1 checksum, generate the corresponding index file, and update the refs) it can easily take several minutes for a single checkpoint command to complete.

Frontends may choose to issue checkpoints during extremely large and long running imports, or when they need to allow another Git process access to a branch. However given that a 30 GiB Subversion repository can be loaded into Git through fast-import in about 3 hours, explicit checkpointing may not be necessary.

The LF after the command is optional (it used to be required).

## progress

Causes fast-import to print the entire progress line unmodified to its standard output channel (file descriptor 1) when the command is processed from the input stream. The command otherwise has no impact on the current import, or on any of fast-import’s internal state.

```
'progress' SP <any> LF LF?
```

The `<any>` part of the command may contain any sequence of bytes that does not contain LF. The LF after the command is optional. Callers may wish to process the output through a tool such as sed to remove the leading part of the line, for example:

```
frontend | git fast-import | sed 's/^progress //'
```

Placing a progress command immediately after a checkpoint will inform the reader when the checkpoint has been completed and it can safely access the refs that fast-import updated.

## cat-blob

Causes fast-import to print a blob to a file descriptor previously arranged with the --cat-blob-fd argument. The command otherwise has no impact on the current import; its main purpose is to retrieve blobs that may be in fast-import's memory but not accessible from the target repository.

```
'cat-blob' SP <dataref> LF
```

The `<dataref>` can be either a mark reference (`:<idnum>`) set previously or a full 40-byte SHA-1 of a Git blob, preexisting or ready to be written.

Output uses the same format as `git cat-file --batch`:

```
<sha1> SP 'blob' SP <size> LF <contents> LF
```

This command can be used anywhere in the stream that comments are accepted. In particular, the cat-blob command can be used in the middle of a commit but not in the middle of a data command.

See “Responses To Commands” below for details about how to read this output safely.

## ls

Prints information about the object at a path to a file descriptor previously arranged with the --cat-blob-fd argument. This allows printing a blob from the active commit (with cat-blob) or copying a blob or tree from a previous commit for use in the current one (with filemodify).

The ls command can be used anywhere in the stream that comments are accepted, including the middle of a commit.

### Reading from the active commit

This form can only be used in the middle of a commit. The path names a directory entry within fast-import's active commit. The path must be quoted in this case.

```
'ls' SP <path> LF
```

### Reading from a named tree

The `<dataref>` can be a mark reference (`:<idnum>`) or the full 40-byte SHA-1 of a Git tag, commit, or tree object, preexisting or waiting to be written. The path is relative to the top level of the tree named by `<dataref>`.

```
'ls' SP <dataref> SP <path> LF
```

See filemodify above for a detailed description of `<path>`.

Output uses the same format as `git ls-tree <tree> -- <path>`:

```
<mode> SP ('blob' | 'tree' | 'commit') SP <dataref> HT <path> LF
```

The `<dataref>` represents the blob, tree, or commit object at `<path>` and can be used in later cat-blob, filemodify, or ls commands.

If there is no file or subtree at that path, git fast-import will instead report:

```
missing SP <path> LF
```

See “Responses To Commands” below for details about how to read this output safely.

## feature

Require that fast-import supports the specified feature, or abort if it does not.

```
'feature' SP <feature> e ('=' <argument>)? LF
```

The `<feature>` part of the command may be any one of the following:

- **date-format**, **export-marks**, **relative-marks**, **no-relative-marks**, **force**
    - Act as though the corresponding command-line option with a leading -- was passed on the command line (see OPTIONS, above).
- **import-marks**, **import-marks-if-exists**
    - Like --import-marks except in two respects: first, only one “feature import-marks” or “feature import-marks-if-exists” command is allowed per stream; second, an --import-marks= or --import-marks-if-exists command-line option overrides any of these “feature” commands in the stream; third, “feature import-marks-if-exists” like a corresponding command-line option silently skips a nonexistent file.
- **cat-blob**, **ls**
    - Require that the backend support the cat-blob or ls command. Versions of fast-import not supporting the specified command will exit with a message indicating so. This lets the import error out early with a clear message, rather than wasting time on the early part of an import before the unsupported command is detected.
- **notes**
    - Require that the backend support the notemodify (N) subcommand to the commit command. Versions of fast-import not supporting notes will exit with a message indicating so.
- **done**
    - Error out if the stream ends without a done command. Without this feature, errors causing the frontend to end abruptly at a convenient point in the stream can go
