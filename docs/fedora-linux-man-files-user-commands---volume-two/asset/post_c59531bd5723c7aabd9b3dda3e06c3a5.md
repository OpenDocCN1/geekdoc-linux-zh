
## SEE ALSO

1. 

## GIT-FORMAT-PATCH

### NAME

git-format-patch - Prepare patches for e-mail submission

### SYNOPSIS

```
git format-patch [-k] [(-o|--output-directory) <dir> | --stdout] [--no-thread | --thread[=<style>]] [(--attach|--inline)[=<boundary>] | --no-attach] [-s | --signoff] [-signatire=<signature> | --no-signature] [signatur-file=<file>] [-n | --numbered | -N | --no-numbered] [--start-number <n>] [--numbered-files] [--in-reply-to=Message-Id] [-<suffix>.<sfx>] [--ignore-if-in-upstream] [--subject-prefix=Subject-Prefix] [(-reroll-count|~-v) <n>] [--to=<email>] [--cc=<email>] [~-[no-]cover-letter] [--quiet] [--notes[=<ref>]] [<common diff options>] [ <since> <revision range> ]
```

### DESCRIPTION

Prepare each commit with its patch in one file per commit, formatted to resemble UNIX mailbox format. The output of this command is convenient for e-mail submission or for use with `git am`.

There are two ways to specify which commits to operate on.

1. A single commit, `<since>`, specifies that the commits leading to the tip of the current branch that are not in the history that leads to the `<since>` to be output.
2. Generic `<revision range>` expression (see “SPECIFYING REVISIONS” section in (7)) means the commits in the specified range.

The first rule takes precedence in the case of a single `<commit>`. To apply the second rule, i.e., format everything since the beginning of history up until `<commit>`, use the `--root` option: `git format-patch --root <commit>`. If you want to format only `<commit>` itself, you can do this with `git format-patch -1 <commit>`.

By default, each output file is numbered sequentially from 1, and uses the first line of the commit message (massaged for pathname safety) as the filename. With the `--numbered-files` option, the output file names will only be numbers, without the first line of the commit appended. The names of the output files are printed to standard output, unless the `--stdout` option is specified.

If `-o` is specified, output files are created in `<dir>`. Otherwise they are created in the current working directory.

By default, the subject of a single patch is “`[PATCH]`” followed by the concatenation of lines from the commit message up to the first blank line (see the DISCUSSION section of (1)).

When multiple patches are output, the subject prefix will instead be “`[PATCH n/m]`”. To force 1/1 to be added for a single patch, use `-n`. To omit patch numbers from the subject, use `-N`.

If given `--thread`, `git-format-patch` will generate In-Reply-To and References headers to make the second and subsequent patch mails appear as replies to the first mail; this also generates a Message-Id header to reference.

### OPTIONS

-   `-p`, `--no-stat`
    Generate plain patches without any diffstats.
-   `-S`, `--no-patch`
    Suppress diff output. Useful for commands like `git show` that show the patch by default, or to cancel the effect of `--patch`.
-   `-U<n>`, `--unified=<n>`
    Generate diffs with `<n>` lines of context instead of the usual three.
-   `--minimal`
    Spend extra time to make sure the smallest possible diff is produced.
-   `--patience`
    Generate a diff using the “patience diff” algorithm.
-   `--histogram`
    Generate a diff using the “histogram diff” algorithm.
-   `--diff-algorithm={patience|minimal|histogram|myers}`
    Choose a diff algorithm. The variants are as follows:
    - **default, myers**: The basic greedy diff algorithm. Currently, this is the default.
    - **minimal**: Spend extra time to make sure the smallest possible diff is produced.
    - **patience**: Use “patience diff” algorithm when generating patches.
    - **histogram**: This algorithm extends the patience algorithm to “support low-occurrence common elements”.

For instance, if you configured `diff.algorithm` variable to a non-default value and want to use the default one, then you have to use `--diff-algorithm=default` option.

-   `--stat[=<width>[,<name-width>[,<count>]]]`
    Generate a diffstat. By default, as much space as necessary will be used for the filename part, and the rest for the graph part. Maximum width defaults to terminal width, or 80 columns if not connected to a terminal, and can be overridden by `<width>`. The width of the filename part can be limited by giving another width
    Name-width> after a comma. The width of the graph part can be limited by using `--stat-graph-width=<width>` (affects all commands generating a stat graph) or by setting `diff.statGraphWidth=<width>` (does not affect git format-patch). By giving a third parameter `<count>`, you can limit the output to the first `<count>` lines, followed by … if there are more.

    These parameters can also be set individually with `--stat-width=<width>`, `--stat-name-width=<name-width>` and `--stat-count=<count>`.

-   `--numstat`
    Similar to `--stat`, but shows number of added and deleted lines in decimal notation and pathname without abbreviation, to make it more machine friendly. For binary files, outputs two `-` instead of saying `0 0`.

-   `--shortstat`
    Output only the last line of the `--stat` format containing total number of modified files, as well as number of added and deleted lines.

-   `--dirstat[=<param1,param2,...>]`
    Output the distribution of relative amount of changes for each sub-directory. The behavior of `--dirstat` can be customized by passing it a comma separated list of parameters. The defaults are controlled by the `diff.dirstat` configuration variable (see (1)). The following parameters are available:
    - `changes`
        Compute the dirstat numbers by counting the lines that have been removed from the source, or added to the destination. This ignores the amount of pure code movements within a file. In other words, rearranging lines in a file is not counted as much as other changes. This is the default behavior when no parameter is given.
    - `lines`
        Compute the dirstat numbers by doing the regular line-based diff analysis, and summing the removed/added line counts. (For binary files, count 64-byte chunks instead, since binary files have no natural concept of lines). This is a more expensive `--dirstat` behavior than the `changes` behavior, but it does count rearranged lines within a file as much as other changes. The resulting output is consistent with what you get from the other `--*stat` options.
    - `files`
        Compute the dirstat numbers by counting the number of files changed. Each changed file counts equally in the dirstat analysis. This is the computationally cheapest `--dirstat` behavior, since it does not have to look at the file contents at all.
    - `cumulative`
        Count changes in a child directory for the parent directory as well. Note that when using cumulative, the sum of the percentages reported may exceed 100%. The default (non-cumulative) behavior can be specified with the `noncumulative` parameter.
    - `<limit>`
        An integer parameter specifies a cut-off percent (3% by default). Directories contributing less than this percentage of the changes are not shown in the output.
    
    Example: The following will count changed files, while ignoring directories with less than 10% of the total amount of changed files, and accumulating child directory counts in the parent directories: `--dirstat=files,10,cumulative`.

-   `--summary`
    Output a condensed summary of extended header information such as creations, renames and mode changes.

-   `--no-renames`
    Turn off rename detection, even when the configuration file gives the default to do so.

-   `--full-index`
    Instead of the first handful of characters, show the full pre- and post-image blob object names on the “index” line when generating patch format output.

-   `--binary`
    In addition to `--full-index`, output a binary diff that can be applied with git-apply.

-   `--abbrev[=<n>]`
    Instead of showing the full 40-byte hexadecimal object name in diff-raw format output and diff-tree header lines, show only a partial prefix. This is independent of the `--full-index` option above, which controls the diff-patch output format. Non default number of digits can be specified with `--abbrev=<n>`.

-   `-B[<n>]/[<m>]`, `--break-rewrites[=[<n>]/[<m>]]`
    Break complete rewrite changes into pairs of delete and create. This serves two purposes:
    
    It affects the way a change that amounts to a total rewrite of a file not as a series of deletion and insertion mixed together with a very few lines that happen to match textually as the context, but as a single deletion of everything old followed by a single insertion of everything new, and the number m controls this aspect of the -B option (defaults to 60%). -B/70% specifies that less than 30% of the original should remain in the result for Git to consider it a total rewrite (i.e. otherwise the resulting patch will be a series of deletion and insertion mixed together with context lines).
    
    When used with -M, a totally-rewritten file is also considered as the source of a rename (usually -M only considers a file that disappeared as the source of a rename), and the number n controls this aspect of the -B option (defaults to 50%). -B20% specifies that a change with addition and deletion compared to 20% or more of the
