# COMBINED DIFF FORMAT

Any diff-generating command can take the -c or —-cc option to produce a combined diff when showing a merge. This is the default format when showing merges with (1) or (1). Note also that you can give the -m option to any of these commands to force generation of diffs with individual parents of a merge.

A combined diff format looks like this:

```
diff --combined describe.c index fabad8b,cc95eb0..4866510 --- a/describe.c +++ b/describe.c @@@ -98,20 -98,12 +98,20 @@@ return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1; } - static void describe(char *arg) -static void describe(struct commit *cmit, int last_one) +static void describe(char *arg, int last_one) { + unsigned char sha1[20]; + struct commit *cmit; struct commit_list *list; static int initialized = 0; struct commit_name *n; + if (get_sha1(arg, sha1) < 0) + usage(describe_usage); + cmit = lookup_commit_reference(sha1); + if (!cmit) + usage(describe_usage); + if (!initialized) { initialized = 1; for_each_ref(get_name);
```

+   1. It is preceded with a "git diff" header, that looks like this (when -c option is used):

```
diff --combined file
```

or like this (when —-cc option is used):

```
diff --cc file
```

+   2. It is followed by one or more extended header lines (this example shows a merge with two parents):

```
index <hash>,<hash>..<hash> mode <mode>,<mode>..<mode> new file mode <mode> deleted file mode <mode>,<mode>
```

The mode <mode>,<mode>..<mode> line appears only if at least one of the <mode> is different from the rest. Extended headers with information about detected contents movement (renames and copying detection) are designed to work with diff of two <tree-ish> and are not used by combined diff format.

+   3. It is followed by two-line from-file/to-file header

```
--- a/file +++ b/file
```

Similar to two-line header for traditional unified diff format, /dev/null is used to signal created or deleted files.

+   4. Chunk header format is modified to prevent people from accidentally feeding it to patch -p1. Combined diff format was created for review of merge commit changes, and was not meant for apply. The change is similar to the change in the extended index header:

```
@@@ <from-file-range> <from-file-range> <to-file-range> @@
```

There are (number of parents + 1) @ characters in the chunk header for combined diff format.