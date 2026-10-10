
Unlike the traditional *unified* diff format, which shows two files A and B with a single column that has `-` (minus – appears in A but removed in B), `+` (plus – missing in A but added to B), or ` ` (space – unchanged) prefix, this format compares two or more files file1, file2,... with one file X, and shows how X differs from each of fileN. One column for each of fileN is prepended to the output line to note how X’s line is different from it. A `-` character in the column N means that the line appears in fileN but it does not appear in the result. A `+` character in the column N means that the line appears in the result, and fileN does not have that line (in other words, the line was added, from the point of view of that parent).

In the above example output, the function signature was changed from both files (hence two `-` removals from both file1 and file2, plus `++` to mean one line that was added does not appear in either file1 or file2). Also eight other lines are the same from file1 but do not appear in file2 (hence prefixed with `+`).

When shown by `git diff-tree -c`, it compares the parents of a merge commit with the merge result (i.e. file1..fileN are the parents). When shown by `git diff-files -c`, it compares the two unresolved merge parents with the working tree file (i.e. file1 is stage 2 aka “our version”, file2 is stage 3 aka “their version”).

## OTHER DIFF FORMATS

The `--summary` option describes newly added, deleted, renamed and copied files.

The `--stat` option adds (1) graph to the output. These options can be combined with other options, such as -p, and are meant for human consumption.

When showing a change that involves a rename or a copy, `--stat` output formats the pathnames compactly by combining common prefix and suffix of the pathnames. For example, a change that moves `arch/i386/Makefile` to `arch/x86/Makefile` while modifying 4 lines will be shown like this:

```
arch/{i386 => x86}/Makefile | 4 +--
```

The `--numstat` option gives the (1) information but is designed for easier machine consumption. An entry in `--numstat` output looks like this:

```
1 2 README 3 1 arch/{i386 => x86}/Makefile
```

That is, from left to right:

- the number of added lines;
- a tab;
- the number of deleted lines;
- a tab;
- pathname (possibly with rename/copy information);
- a newline.

When -z output option is in effect, the output is formatted this way:

```
1 2 README NUL 3 1 NUL arch/i386/Makefile NUL arch/x86/Makefile NUL
```

That is:

- the number of added lines;
- a tab;
- the number of deleted lines;
- a tab;
- a NUL (only exists if renamed/copied);
- pathname in preimage;
- a NUL (only exists if renamed/copied);
- pathname in postimage (only exists if renamed/copied);
- a NUL.

The extra NUL before the preimage path in renamed case is to allow scripts that read the output to tell if the current record being read is a single-path record or a rename/copy record without reading ahead. After reading added and deleted lines, reading up to NUL would yield the pathname, but if that is NUL, the record will show two paths.

## GIT-DIFF-INDEX

### NAME

`git-diff-index` - Compare a tree to the working tree or index

### SYNOPISIS

```
git diff-index [-m] [--cached] [<common diff options>] <tree-ish>
[<path>...]
```

### DESCRIPTION

Compares the content and mode of the blobs found in a tree object with the corresponding tracked files in the working tree, or with the corresponding paths in the index. When <path> arguments are present, compares only paths matching those patterns. Otherwise all tracked files are compared.

### OPTIONS

-p, -u, --patch
Generate patch (see section on generating patches).

-S, --no-patch
Suppress diff output. Useful for commands like git show that show the patch by default, or to cancel the effect of --patch.

-U<n>, --unified=<n>
Generate diffs with <n> lines of context instead of the usual three. Implies -p.

--raw
Generate the diff in raw format. This is the default.

--patch-with-raw
Synonym for -p --raw.

--minimal
Spend extra time to make sure the smallest possible diff is produced.

--patience
Generate a diff using the “patience diff” algorithm.

--histogram
Generate a diff using the “histogram diff” algorithm.

--diff-algorithm={patience|minimal|histogram|myers}
Choose a diff algorithm. The variants are as follows:

- default, myers
The basic greedy diff algorithm. Currently, this is the default.

- minimal
Spend extra time to make sure the smallest possible diff is produced.

- patience
Use “patience diff” algorithm when generating patches.

- histogram
This algorithm extends the patience algorithm to “support low-occurrence common elements”.

For instance, if you configured diff.algorithm variable to a non-default value and want to use the default one, then you have to use --diff-algorithm=default option.

--stat[=<width>,<name-width>[,<count>]]
Generate a diffstat. By default, as much space as necessary will be used for the filename part, and the rest for the graph part. Maximum width defaults to terminal width, or 80 columns if not connected to a terminal, and can be overridden by <width>. The width of the filename part can be limited by giving another width <name-width> after a comma. The width of the graph part can be limited by using --stat-graph-width=<width> (affects all commands generating a stat graph) or by setting diff.statGraphWidth=<width> (does not affect git format-patch). By giving a third parameter <count>, you can limit the output to the first <count> lines, followed by ... if there are more.

These parameters can also be set individually with --stat-width=<width>, --stat-name-width=<name-width> and --stat-count=<count>.

--numstat
Similar to --stat, but shows number of added and deleted lines in decimal notation and pathname without abbreviation, to make it more machine friendly. For binary files, outputs two - instead of saying 0 0.

--shortstat
Output only the last line of the --stat format containing total number of modified files, as well as number of added and deleted lines.

--dirstat[=<param1,param2,...>]
Output the distribution of relative amount of changes for each sub-directory. The behavior of --dirstat can be customized by passing it a comma separated list of parameters. The defaults are controlled by the diff.dirstat configuration variable (see (1)). The following parameters are available:

- changes
Compute the dirstat numbers by counting the lines that have been removed from the source, or added to the destination. This ignores the amount of pure code movements within a file. In other words, rearranging lines in a file is not counted as much as other changes. This is the default behavior when no parameter is given.

- lines
Compute the dirstat numbers by doing the regular line-based diff analysis, and summing the removed/added line counts. (For binary files, count 64-byte chunks instead, since binary files have no natural concept of lines). This is a more expensive --dirstat behavior than the changes behavior, but it does count rearranged lines within a file as much as other changes. The resulting output is consistent with what you get from the other --*stat options.

- files
Compute the dirstat numbers by counting the number of files changed. Each changed file counts equally in the dirstat analysis. This is the computationally cheapest --dirstat behavior, since it does not have to look at the file contents at all.

- cumulative
Count changes in a child directory for the parent directory as well. Note that when using cumulative, the sum of the percentages reported may exceed 100%. The default (non-cumulative) behavior can be specified with the noncumulative parameter.

- <limit>
An integer parameter specifies a cut-off percent (3% by default). Directories contributing less than this percentage of the changes are not shown in the output.

Example: The following will count changed files, while ignoring directories with less than 10% of the total amount of changed files, and accumulating child directory counts in the parent directories: --dirstat=files,10,cumulative.

--summary
Output a condensed summary of extended header information such as creations, renames and mode changes.

--patch-with-stat
Synonym for -p --stat.

-z
When --raw, --numstat, --name-only or --name-status has been given, do not munge pathnames and use NULs as output field terminators.

Without this option, each pathname output will have TAB, LF, double quotes, and backslash characters replaced with \t, \n, ", and \\, respectively, and the pathname will be enclosed in double quotes if any of those replacements occurred.

--name-only
Show only names of changed files.

--name-status
Show only names and status of changed files. See the description of the --diff-filter option on what the status letters mean.

--submodule[=<format>]
Specify how differences in submodules are shown. When --submodule or --submodule=log is given, the log format is used. This format lists the commits in the range like (1)summary does. Omitting the --submodule option or specifying --submodule=short, uses the short format. This format just shows the names of the commits at the beginning and end of the range. Can be tweaked via the diff.submodule configuration variable.

--color[=<when>]
