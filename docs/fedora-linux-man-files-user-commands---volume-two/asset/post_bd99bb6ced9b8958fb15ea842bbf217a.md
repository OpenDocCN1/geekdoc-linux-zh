
Equivalent to `--word-diff=color` plus (if a regex was specified) `--word-diff-regex=<regex>`.

## --no-renames

Turn off rename detection, even when the configuration file gives the default to do so.

## --check

Warn if changes introduce whitespace errors. What are considered whitespace errors is controlled by `core.whitespace` configuration. By default, trailing whitespaces (including lines that solely consist of whitespaces) and a space character that is immediately followed by a tab character inside the initial indent of the line are considered whitespace errors. Exits with non-zero status if problems are found. Not compatible with `--exit-code`.

## --ws-error-highlight=<kind>

Highlight whitespace errors on lines specified by `<kind>` in the color specified by `color.diff.whitespace`. `<kind>` is a comma separated list of `old`, `new`, `context`. When this option is not given, only whitespace errors in new lines are highlighted. E.g. `--ws-error-highlight=new,old` highlights whitespace errors on both deleted and added lines. `all` can be used as a short-hand for `old,new,context`.

## --full-index

Instead of the first handful of characters, show the full pre- and post-image blob object names on the “index” line when generating patch format output.

## --binary

In addition to `--full-index`, output a binary diff that can be applied with `git-apply`.

## --abbrev[=<n>]

Instead of showing the full 40-byte hexadecimal object name in diff-raw format output and diff-tree header lines, show only a partial prefix. This is independent of the `--full-index` option above, which controls the diff-patch output format. Non default number of digits can be specified with `--abbrev=<n>`.

## -B[<n>[/ <m>]], --break-rewrites[=<n>[/ <m>]]

Break complete rewrite changes into pairs of delete and create. This serves two purposes:

It affects the way a change that amounts to a total rewrite of a file not as a series of deletion and insertion mixed together with a very few lines that happen to match textually as the context, but as a single deletion of everything old followed by a single insertion of everything new, and the number `m` controls this aspect of the `-B` option (defaults to 60%). `-B/70%` specifies that less than 30% of the original should remain in the result for Git to consider it a total rewrite (i.e. otherwise the resulting patch will be a series of deletion and insertion mixed together with context lines).

When used with `-M`, a totally-rewritten file is also considered as the source of a rename (usually `-M` only considers a file that disappeared as the source of a rename), and the number `n` controls this aspect of the `-B` option (defaults to 50%). `-B20%` specifies that a change with addition and deletion compared to 20% or more of the file’s size are eligible for being picked up as a possible source of a rename to another file.

## -M[<n>], --find-renames[=<n>]

If generating diffs, detect and report renames for each commit. For following files across renames while traversing history, see `--follow`. If `n` is specified, it is a threshold on the similarity index (i.e. amount of addition/deletions compared to the file’s size). For example, `-M90%` means Git should consider a delete/add pair to be a rename if more than 90% of the file hasn’t changed. Without a % sign, the number is to be read as a fraction, with a decimal point before it. I.e., `-M5` becomes 0.5, and is thus the same as `-M50%`. Similarly, `-M05` is the same as `-M5%`. To limit detection to exact renames, use `-M100%`. The default similarity index is 50%.

## -C[<n>], --find-copies[=<n>]

Detect copies as well as renames. See also `--find-copies-harder`. If `n` is specified, it has the same meaning as for `-M<n>`.

## --find-copies-harder

For performance reasons, by default, `-C` option finds copies only if the original file of the copy was modified in the same changeset. This flag makes the command inspect unmodified files as candidates for the source of copy. This is a very expensive operation for large projects, so use it with caution. Giving more than one `-C` option has the same effect.

## -D, --irreversible-delete

Omit the preimage for deletes, i.e. print only the header but not the diff between the preimage and /dev/null. The resulting patch is not meant to be applied with patch or git apply; this is solely for people who want to just concentrate on reviewing the text after the change. In addition, the output obviously lack enough information to apply such a patch in reverse, even manually, hence the name of the option.

When used together with `-B`, omit also the preimage in the deletion part of a delete/create pair.

## -l<num>

The `-M` and `-C` options require O(n^2) processing time where n is the number of potential rename/copy targets. This option prevents rename/copy detection from running if the number of rename/copy targets exceeds the specified number.

## --diff-filter=([A|C|D|M|R|T|U|X|B]...[*])

Select only files that are Added (A), Copied (C), Deleted (D), Modified (M), Renamed (R), have their type (i.e. regular file, symlink, submodule, …) changed (T), are Unmerged (U), are Unknown (X), or have had their pairing Broken (B). Any combination of the filter characters (including none) can be used. When * (All-or-none) is added to the combination, all paths are selected if there is any file that matches other criteria in the comparison; if there is no file that matches other criteria, nothing is selected.

## -S<string>

Look for differences that change the number of occurrences of the specified string (i.e. addition/deletion) in a file. Intended for the scripter’s use.

It is useful when you’re looking for an exact block of code (like a struct), and want to know the history of that block since it first came into being: use the feature iteratively to feed the interesting block in the preimage back into `-S`, and keep going until you get the very first version of the block.

## -G<regex>

Look for differences whose patch text contains added/removed lines that match `<regex>`.

To illustrate the difference between `-S<regex>`—pickaxe-regex and `-G<regex>`, consider a commit with the following diff in the same file:

```
+ \!regexec( regexp, two->ptr, 1, &regexpmatch, 0); ... - hit = !\!regexec( regexp, mf2.ptr, 1, &regexpmatch, 0);
```

While git log -G"regexec(regexp)" will show this commit, git log -S"regexec(regexp)"—pickaxe-regex will not (because the number of occurrences of that string did not change). See the *pickaxe* entry in (7) for more information.

## --pickaxe-all

When `-S` or `-G` finds a change, show all the changes in that changeset, not just the files that contain the change in `<string>`.

## --pickaxe-regex

Treat the `<string>` given to `-S` as an extended POSIX regular expression to match.

## -O<orderfile>

Output the patch in the order specified in the `<orderfile>`, which has one shell glob pattern per line. This overrides the `diff.orderFile` configuration variable (see (1)). To cancel `diff.orderFile`, use `-O/dev/null`.

## -R

Swap two inputs; that is, show differences from index or on-disk file to tree contents.

## --relative[=<path>]

When run from a subdirectory of the project, it can be told to exclude changes outside the directory and show pathnames relative to it with this option. When you are not in a subdirectory (e.g. in a bare repository), you can name which subdirectory to make the output relative to by giving a `<path>` as an argument.

## -a, --text

Treat all files as text.

## --ignore-space-at-eol

Ignore changes in whitespace at EOL.

## -b, --ignore-space-change

Ignore changes in amount of whitespace. This ignores whitespace at line end, and considers all other sequences of one or more whitespace characters to be equivalent.

## -w, --ignore-all-space

Ignore whitespace when comparing lines. This ignores differences even if one line has whitespace where the other line has none.

## --ignore-blank-lines

Ignore changes whose lines are all blank.

## --inter-hunk-context=<lines>

Show the context between diff hunks, up to the specified number of lines, thereby fusing hunks that are close to each other.

## -W, --function-context

Show whole surrounding functions of changes.

## --ext-diff

Allow an external diff helper to be executed. If you set an external diff driver with (5), you need to use this option with (1) and friends.

## --no-ext-diff

Disallow external diff drivers.

## --textconv, --no-textconv

Allow (or disallow) external text conversion filters to be run when comparing binary files. See (5) for details. Because textconv filters are typically a one-way conversion, the resulting diff is suitable for human consumption, but cannot be applied. For this reason, textconv filters are enabled by default only for (1) and (1), but not for (1) or diff plumbing commands.

## --ignore-submodules[=<when>]

Ignore changes to submodules in the diff generation. `<when>` can be either “none”, “untracked”, “dirty” or “all”, which is the default. Using “none” will consider the submodule modified when it either contains untracked or modified files or its HEAD differs from the commit recorded in the superproject and can be used to override any settings of the ignore option in (1) or (5). When “untracked” is used submodules are
