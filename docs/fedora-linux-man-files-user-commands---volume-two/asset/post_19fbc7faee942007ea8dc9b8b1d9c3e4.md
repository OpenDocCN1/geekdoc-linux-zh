
## DIFF FORMAT FOR MERGES

“git-diff-tree”, “git-diff-files” and “git-diff --raw” can take -c or --cc option to generate diff output also for merge commits. The output differs from the format described above in the following way:

1. there is a colon for each parent
2. there are more “src” modes and “src” sha1
3. status is concatenated status characters for each parent
4. no optional “score” number
5. single path, only for “dst”

Example:
`::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM describe.c`

Note that combined diff lists only files which were modified from all parents.

## GENERATING PATCHES WITH -p

When “git-diff-index”, “git-diff-tree”, or “git-diff-files” are run with a -p option, “git diff” without the --raw option, or “git log” with the “-p” option, they do not produce the output described above; instead they produce a patch file. You can customize the creation of such patches via the GIT_EXTERNAL_DIFF and the GIT_DIFF_OPTS environment variables.

What the -p option produces is slightly different from the traditional diff format:

1. It is preceded with a “git diff” header that looks like this:

   ```
   diff --git a/file1 b/file2
   ```

   The a/ and b/ filenames are the same unless rename/copy is involved. Especially, even for a creation or a deletion, /dev/null is not used in place of the a/ or b/ filenames.

   When rename/copy is involved, file1 and file2 show the name of the source file of the rename/copy and the name of the file that rename/copy produces, respectively.

2. It is followed by one or more extended header lines:

   ```
   old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>
   ```

   File modes are printed as 6-digit octal numbers including the file type and file permission bits.

   Path names in extended headers do not include the a/ and b/ prefixes.

   The similarity index is the percentage of unchanged lines, and the dissimilarity index is the percentage of changed lines. It is a rounded down integer, followed by a percent sign. The similarity index value of 100% is thus reserved for two equal files, while 100% dissimilarity means that no line from the old file made it into the new one.

   The index line includes the SHA-1 checksum before and after the change. The <mode> is included if the file mode does not change; otherwise, separate lines indicate the old and the new mode.

3. TAB, LF, double quote and backslash characters in pathnames are represented as \t, \n, \" and \\, respectively. If there is need for such substitution then the whole pathname is put in double quotes.

4. All the file1 files in the output refer to files before the commit, and all the file2 files refer to files after the commit. It is incorrect to apply each change to each file sequentially. For example, this patch will swap a and b:

   ```
   diff --git a/a b/b rename from a rename to b diff --git a/b b/a rename from b rename to a
   ```

## COMBINED DIFF FORMAT

Any diff-generating command can take the -c or --cc option to produce a combined diff when showing a merge. This is the default format when showing merges with `git diff-tree` or `git diff-files`. Note also that you can give the -m option to any of these commands to force generation of diffs with individual parents of a merge.

A combined diff format looks like this:

```
diff --combined describe.c index fabad8b,cc95eb0..4866510 --- a/describe.c +++ b/describe.c @@@ -98,20 -98,12 +98,20 @@@ return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1; } - static void describe(char *arg) -static void describe(struct commit *cmit, int last_one) +static void describe(char *arg, int last_one) { + unsigned char sha1[20]; + struct commit *cmit; struct commit_list *list; static int initialized = 0; struct commit_name *n; + if (get_sha1(arg, sha1) < 0) + usage(describe_usage); + cmit = lookup_commit_reference(sha1); + if (!cmit) + usage(describe_usage); + if (!initialized) { initialized = 1; for_each_ref(get_name);
```

1. It is preceded with a "git diff" header, that looks like this (when -c option is used):

   ```
   diff --combined file
   ```

   or like this (when --cc option is used):

   ```
   diff --cc file
   ```

2. It is followed by one or more extended header lines (this example shows a merge with two parents):

   ```
   index <hash>,<hash>..<hash> mode <mode>,<mode>..<mode> new file mode <mode> deleted file mode <mode>,<mode>
   ```

   The mode <mode>,<mode>..<mode> line appears only if at least one of the <mode> is different from the rest. Extended headers with information about detected contents movement (renames and copying detection) are designed to work with diff of two <tree-ish> and are not used by combined diff format.

3. It is followed by two-line from-file/to-file header

   ```
   --- a/file +++ b/file
   ```

   Similar to two-line header for traditional unified diff format, /dev/null is used to signal created or deleted files.

4. Chunk header format is modified to prevent people from accidentally feeding it to patch -p1. Combined diff format was created for review of merge commit changes, and was not meant for apply. The change is similar to the change in the extended index header:

   ```
   @@@ <from-file-range> <from-file-range> <to-file-range> @
   ```

   There are (number of parents + 1) @ characters in the chunk header for combined diff format.

Unlike the traditional *unified* diff format, which shows two files A and B with a single column that has - (minus – appears in A but removed in B), + (plus – missing in A but added to B), or “ ” (space – unchanged) prefix, this format compares two or more files file1, file2,... with one file X, and shows how X differs from each of fileN. One column for each of fileN is prepended to the output line to note how X’s line is different from it. A - character in the column N means that the line appears in fileN but it does not appear in the result. A + character in the column N means that the line appears in the result, and fileN does not have that line (in other words, the line was added, from the point of view of that parent).

In the above example output, the function signature was changed from both files (hence two - removals from both file1 and file2, plus ++ to mean one line that was added does not appear in either file1 or file2). Also eight other lines are the same from file1 but do not appear in file2 (hence prefixed with +).

When shown by git diff-tree -c, it compares the parents of a merge commit with the merge result (i.e. file1..fileN are the parents). When shown by git diff-files -c, it compares the two unresolved merge parents with the working tree file (i.e. file1 is stage 2 aka “our version”, file2 is stage 3 aka “their version”).

## OTHER DIFF FORMATS

The `--summary` option describes newly added, deleted, renamed and copied files.

The `--stat` option adds a graph to the output. These options can be combined with other options, such as -p, and are meant for human consumption.

When showing a change that involves a rename or a copy, `--stat` output formats the pathnames compactly by combining common prefix and suffix of the pathnames. For example, a change that moves `arch/i386/Makefile` to `arch/x86/Makefile` while modifying 4 lines will be shown like this:

```
arch/{i386 => x86}/Makefile | 4 +--
```

The `--numstat` option gives the numerical information but is designed for easier machine consumption. An entry in `--numstat` output looks like this:

```
1 2 README 3 1 arch/{i386 => x86}/Makefile
```

That is, from left to right:

1. the number of added lines;
2. a tab;
3. the number of deleted lines;
4. a tab;
5. pathname (possibly with rename/copy information);
6. a newline.

When -z output option is in effect, the output is formatted this way:

```
1 2 README NUL 3 1 NUL arch/i386/Makefile NUL arch/x86/Makefile NUL
```

That is:

1. the number of added lines;
2. a tab;
3. the number of deleted lines;
4. a tab;
5. a NUL (only exists if renamed/copied);
6. pathname in preimage;
7. a NUL (only exists if renamed/copied);
8. pathname in postimage (only exists if renamed/copied);
9. a NUL.

The extra NUL before the preimage path in renamed case is to allow scripts that read the output to tell if the current record being read is a single-path record or a rename/copy
