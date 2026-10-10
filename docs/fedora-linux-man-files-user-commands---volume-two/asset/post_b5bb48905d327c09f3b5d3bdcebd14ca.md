
combination of the filter characters (including none) can be used. When `*` (All-or-none) is added to the combination, all paths are selected if there is any file that matches other criteria in the comparison; if there is no file that matches other criteria, nothing is selected.

### -S<string>

Look for differences that change the number of occurrences of the specified string (i.e. addition/deletion) in a file. Intended for the scripter’s use.

It is useful when you’re looking for an exact block of code (like a struct), and want to know the history of that block since it first came into being; use the feature iteratively to feed the interesting block in the preimage back into -S, and keep going until you get the very first version of the block.

### -G<regex>

Look for differences whose patch text contains added/removed lines that match `<regex>`.

To illustrate the difference between `-S<regex>` —pickaxe-regex and `-G<regex>`, consider a commit with the following diff in the same file:

```text
+ return !regexexec(regexp, two->ptr, 1, &regmatch, 0); . . . - hit =
!regexexec(regexp, mf2.ptr, 1, &regmatch, 0);
```

While `git log -G"regexec(regexp)"` will show this commit, `git log -S"regexec(regexp)"` —pickaxe-regex will not (because the number of occurrences of that string did not change). See the pickaxe entry in (7) for more information.

### --pickaxe-all

When -S or -G finds a change, show all the changes in that changeset, not just the files that contain the change in `<string>`.

### --pickaxe-regex

Treat the `<string>` given to -S as an extended POSIX regular expression to match.

### -O<orderfile>

Output the patch in the order specified in the `<orderfile>`, which has one shell glob pattern per line. This overrides the `diff.orderFile` configuration variable (see (1)). To cancel `diff.orderFile`, use `-O /dev/null`.

### -R

Swap two inputs; that is, show differences from index or on-disk file to tree contents.

### --relative[<=<path>]

When run from a subdirectory of the project, it can be told to exclude changes outside the directory and show pathnames relative to it with this option. When you are not in a subdirectory (e.g. in a bare repository), you can name which subdirectory to make the output relative to by giving a `<path>` as an argument.

### -a, --text

Treat all files as text.

### --ignore-space-at-eol

Ignore changes in whitespace at EOL.

### -b, --ignore-space-change

Ignore changes in amount of whitespace. This ignores whitespace at line end, and considers all other sequences of one or more whitespace characters to be equivalent.

### -w, --ignore-all-space

Ignore whitespace when comparing lines. This ignores differences even if one line has whitespace where the other line has none.

### --ignore-blank-lines

Ignore changes whose lines are all blank.

### --inter-hunk-context=<lines>

Show the context between diff hunks, up to the specified number of lines, thereby fusing hunks that are close to each other.

### -W, --function-context

Show whole surrounding functions of changes.

### --exit-code

Make the program exit with codes similar to (1). That is, it exits with 1 if there were differences and 0 means no differences.

### --quiet

Disable all output of the program. Implies --exit-code.

### --ext-diff

Allow an external diff helper to be executed. If you set an external diff driver with (5), you need to use this option with (1) and friends.

### --no-ext-diff

Disallow external diff drivers.

### --textconv, --no-textconv

Allow (or disallow) external text conversion filters to be run when comparing binary files. See (5) for details. Because textconv filters are typically a one-way conversion, the resulting diff is suitable for human consumption, but cannot be applied. For this reason, textconv filters are enabled by default only for (1) and (1), but not for (1) or diff plumbing commands.

### --ignore-submodules[=<when>]

Ignore changes to submodules in the diff generation. `<when>` can be either “none”, “untracked”, “dirty” or “all”, which is the default. Using “none” will consider the submodule modified when it either contains untracked or modified files or its HEAD differs from the commit recorded in the superproject and can be used to override any settings of the *ignore* option in (1) or (5). When “untracked” is used submodules are not considered dirty when they only contain untracked content (but they are still scanned for modified content). Using “dirty” ignores all changes to the work tree of submodules, only changes to the commits stored in the superproject are shown (this was the behavior until 1.7.0). Using “all” hides all changes to submodules.

### --src-prefix=<prefix>

Show the given source prefix instead of “a/”.

### --dst-prefix=<prefix>

Show the given destination prefix instead of “b/”.

### --no-prefix

Do not show any source or destination prefix.

For more detailed explanation on these common options, see also (7).

### <path>...

The `<paths>` parameters, when given, are used to limit the diff to the named paths (you can give directory names and get diff for all files under them).

## RAW OUTPUT FORMAT

The raw output format from “git-diff-index”, “git-diff-tree”, “git-diff-files” and “git diff --raw” are very similar.

These commands all compare two sets of things; what is compared differs:

```
git-diff-index <tree-ish>
```

compares the `<tree-ish>` and the files on the filesystem.

`git-diff-index --cached <tree-ish>`

compares the `<tree-ish>` and the index.

```
git-diff-tree [-r] <tree-ish-1> <tree-ish-2> [pattern>…]
```

compares the trees named by the two arguments.

```
git-diff-files [<pattern>…]
```

compares the index and the files on the filesystem.

The “git-diff-tree” command begins its output by printing the hash of what is being compared. After that, all the commands print one output line per changed file.

An output line is formatted this way:

```
in-place edit :100644 100644 bcd1234… 0123456… M file0
copy-edit :100644 100644 abcd123… 1234567… C68 file1 file2
rename-edit :100644 100644 abcd123… 1234567… R86 file1 file3
create :000000 100644 000000… 1234567… A file4
delete :100644 000000 1234567… 0000000… D file5
unmerged :000000 000000 0000000… 0000000… U file6
```

That is, from the left to the right:

1. a colon.
2. mode for “src”; 000000 if creation or unmerged.
3. a space.
4. mode for “dst”; 000000 if deletion or unmerged.
5. a space.
6. sha1 for “src”; 0{40} if creation or unmerged.
7. a space.
8. sha1 for “dst”; 0{40} if creation, unmerged or “look at work tree”.
9. a space.
10. status, followed by optional “score” number.
11. a tab or a NUL when -z option is used.
12. path for “src”
13. a tab or a NUL when -z option is used; only exists for C or R.
14. path for “dst”; only exists for C or R.
15. an LF or a NUL when -z option is used, to terminate the record.

Possible status letters are:

- A: addition of a file
- C: copy of a file into a new one
- D: deletion of a file
- M: modification of the contents or mode of a file
- R: renaming of a file
- T: change in the type of the file
- U: file is unmerged (you must complete the merge before it can be committed)
- X: “unknown” change type (most probably a bug, please report it)

Status letters C and R are always followed by a score (denoting the percentage of similarity between the source and target of the move or copy). Status letter M may be followed by a score (denoting the percentage of dissimilarity) for file rewrites.

`<sha1>` is shown as all 0’s if a file is new on the filesystem and it is out of sync with the index.

Example:

```
:100644 100644 5be4a4.... 000000.... M file.c
```

When -z option is not used, TAB, LF, and backslash characters in pathnames are represented as `\t`, `\n`, and `\`, respectively.
