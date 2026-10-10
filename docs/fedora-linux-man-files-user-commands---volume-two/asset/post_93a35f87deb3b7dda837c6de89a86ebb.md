
## OTHER DIFF FORMATS

The `--summary` option describes newly added, deleted, renamed and copied files.

The `--stat` option adds a graph to the output. These options can be combined with other options, such as `-p`, and are meant for human consumption.

When showing a change that involves a rename or a copy, `--stat` output formats the pathnames compactly by combining common prefix and suffix of the pathnames. For example, a change that moves `arch/i386/Makefile` to `arch/x86/Makefile` while modifying 4 lines will be shown like this:

```
arch/{i386 => x86}/Makefile | 4 +--
```

The `--numstat` option gives the statistical information but is designed for easier machine consumption. An entry in `--numstat` output looks like this:

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

When `-z` output option is in effect, the output is formatted this way:

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

## GIT-DIFF

### NAME

git-diff - Show changes between commits, commit and working tree, etc

### SYNOPSIS

```
git diff [options] [<commit> [---] [<path>...]]
git diff [options] --cached [<commit>]
git diff [options] <commit> <commit>
git diff [options] <commit> <commit> [--] [<path>...]
git diff [options] <blob> <blob>
git diff [options] [--no-index] [--] <path> <path>
```

### DESCRIPTION

Show changes between the working tree and the index or a tree, changes between the index and a tree, changes between two trees, changes between two blob objects, or changes between two files on disk.

`*git diff* [options] [---] [<path>...]`

This form is to view the changes you made relative to the index (staging area for the next commit). In other words, the differences are what you *could* tell Git to further add to the index but you still haven’t. You can stage these changes by using `git add`.

`*git diff* --no-index [options] [---] [<path>...]`

This form is to compare the given two paths on the filesystem. You can omit the `--no-index` option when running the command in a working tree controlled by Git and at least one of the paths points outside the working tree, or when running the command outside a working tree controlled by Git.

`*git diff* [options] --cached [<commit>] [---] [<path>...]`

This form is to view the changes you staged for the next commit relative to the named `<commit>`. Typically you would want comparison with the latest commit, so if you do not give `<commit>`, it defaults to HEAD. If HEAD does not exist (e.g. unborn branches) and `<commit>` is not given, it shows all staged changes. `--staged` is a synonym of `--cached`.

`*git diff* [options] <commit> [---] [<path>...]`

This form is to view the changes you have in your working tree relative to the named `<commit>`. You can use HEAD to compare it with the latest commit, or a branch name to compare with the tip of a different branch.

`*git diff* [options] <commit> <commit> [---] [<path>...]`

This is to view the changes between two arbitrary `<commit>`s.

`*git diff* [options] <commit>..<commit> [---] [<path>...]`

This is synonymous to the previous form. If `<commit>` on one side is omitted, it will have the same effect as using HEAD instead.

`*git diff* [options] <commit>...<commit> [---] [<path>...]`

This form is to view the changes on the branch containing and up to the second `<commit>`, starting at a common ancestor of both `<commit>`s. “git diff A...B” is equivalent to “git diff $(git-merge-base A B) B”. You can omit any one of `<commit>`s, which has the same effect as using HEAD instead.

Just in case if you are doing something exotic, it should be noted that all of the `<commit>` in the above description, except in the last two forms that use “..” notations, can be any `<tree>`.

For a more complete list of ways to spell `<commit>`, see “SPECIFYING REVISIONS” section in `gitglossary(7)`. However, “diff” is about comparing two *endpoints*, not ranges, and the range notations (“`<commit>..<commit>`” and “`<commit>...<commit>`”) do not mean a range as defined in the “SPECIFYING RANGES” section in `gitglossary(7)`.

`git diff [options] <blob> <blob>`

This form is to view the differences between the raw contents of two blob objects.

### OPTIONS

- `-p, -u, --patch`
  - Generate patch (see section on generating patches). This is the default.
- `-S, --no-patch`
  - Suppress diff output. Useful for commands like git show that show the patch by default, or to cancel the effect of `--patch`.
- `-U<n>, --unified=<n>`
  - Generate diffs with `<n>` lines of context instead of the usual three. Implies `-p`.
- `--raw`
  - Generate the diff in raw format.
- `--patch-with-raw`
  - Synonym for `-p --raw`.
- `--minimal`
  - Spend extra time to make sure the smallest possible diff is produced.
- `--patience`
  - Generate a diff using the “patience diff” algorithm.
- `--histogram`
  - Generate a diff using the “histogram diff” algorithm.
- `--diff-algorithm={patience|minimal|histogram|myers}`
  - Choose a diff algorithm. The variants are as follows:
    - `default, myers`
      - The basic greedy diff algorithm. Currently, this is the default.
    - `minimal`
      - Spend extra time to make sure the smallest possible diff is produced.
    - `patience`
      - Use “patience diff” algorithm when generating patches.
    - `histogram`
      - This algorithm extends the patience algorithm to “support low-occurrence common elements”.

For instance, if you configured `diff.algorithm` variable to a non-default value and want to use the default one, then you have to use `--diff-algorithm=default` option.

`--stat[=<width>,<name-width>[,<count>]]`

Generate a diffstat. By default, as much space as necessary will be used for the filename part, and the rest for the graph part. Maximum width defaults to terminal width, or 80 columns if not connected to a terminal, and can be overridden by `<width>`. The width of the filename part can be limited by giving another width `<name-width>` after a comma. The width of the graph part can be limited by using `--stat-graph-width=<width>` (affects all commands generating a stat graph) or by setting `diff.statGraphWidth=<width>` (does not affect `git format-patch`). By giving a third parameter `<count>`, you can limit the output to the first `<count>` lines, followed by `...` if there are more.

These parameters can also be set individually with `--stat-width=<width>`, `--stat-name-width=<name-width>` and `--stat-count=<count>`.

`--numstat`

Similar to `--stat`, but shows number of added and deleted lines in decimal notation and pathname without abbreviation, to make it more machine friendly. For binary files, outputs two `-` instead of saying `0 0`.

`--shortstat`

Output only the last line of the `--stat` format containing total number of modified files, as well as number of added and deleted lines.

`--dirstat[=<param1,param2,...>]`

Output the distribution of relative amount of changes for each sub-directory. The behavior of `--dirstat` can be customized by passing it a comma separated list of parameters. The defaults are controlled by the `diff.dirstat` configuration variable (see `git-config(1)`). The following parameters are available:

- `changes`
  - Compute the dirstat numbers by counting the lines that have been removed from the source, or added to the destination. This ignores the amount of pure code movements within a file. In other words, rearranging lines in a file is not counted as much as other changes. This is the default behavior when no parameter is given.
- `lines`
  - Compute the dirstat numbers by doing the regular line-based diff analysis, and summing the removed/added line counts. (For binary files, count 64-byte chunks instead, since binary files have no natural concept of lines). This is a more expensive `--dirstat` behavior than the `changes` behavior, but it does count rearranged lines within a file as much as other changes. The resulting output is consistent with what you get from the other `--*stat` options.
- `files`
  - Compute the dirstat numbers by counting the number of files changed. Each changed
