
## git diff-tree / git log Options

“untracked”, “dirty” or “all”, which is the default. Using “none” will consider the submodule modified when it either contains untracked or modified files or its HEAD differs from the commit recorded in the superproject and can be used to override any settings of the *ignore* option in (1) or (5). When “untracked” is used submodules are not considered dirty when they only contain untracked content (but they are still scanned for modified content). Using “dirty” ignores all changes to the work tree of submodules, only changes to the commits stored in the superproject are shown (this was the behavior until 1.7.0). Using “all” hides all changes to submodules.

- `--src-prefix=<prefix>`

Show the given source prefix instead of ‘a/’.

- `--dst-prefix=<prefix>`

Show the given destination prefix instead of ‘b/’.

- `--no-prefix`

Do not show any source or destination prefix.

For more detailed explanation on these common options, see also (7).

- `<tree-ish>`

The id of a tree object.

- `<path>...`

If provided, the results are limited to a subset of files matching one of these prefix strings. i.e., file matches `/<pattern1>|<pattern2>|.../` Note that this parameter does not provide any wildcard or regexp features.

- `-r`

recurse into sub-trees

- `-t`

show tree entry itself as well as subtrees. Implies `-r`.

- `--root`

When `--root` is specified the initial commit will be shown as a big creation event. This is equivalent to a diff against the NULL tree.

- `--stdin`

When `--stdin` is specified, the command does not take `<tree-ish>` arguments from the command line. Instead, it reads lines containing either two `<tree>`, one `<commit>`, or a list of `<commit>` from its standard input. (Use a single space as separator.)

When two trees are given, it compares the first tree with the second. When a single commit is given, it compares the commit with its parents. The remaining commits, when given, are used as if they are parents of the first commit.

When comparing two trees, the ID of both trees (separated by a space and terminated by a newline) is printed before the difference. When comparing commits, the ID of the first (or only) commit, followed by a newline, is printed.

The following flags further affect the behavior when comparing commits (but not trees).

- `-m`

By default, git diff-tree --stdin does not show differences for merge commits. With this flag, it shows differences to that commit from all of its parents. See also -c.

- `-S`

By default, git diff-tree --stdin shows differences, either in machine-readable form (without -p) or in patch form (with -p). This output can be suppressed. It is only useful with -v flag.

- `-v`

This flag causes git diff-tree --stdin to also show the commit message before the differences.

- `--pretty[=<format>], --format=<format>`

Pretty-print the contents of the commit logs in a given format, where <format> can be one of oneline, short, medium, full, fuller, email, raw, format: <string> and format: <string>. When <format> is none of the above, and has %placeholder in it, it acts as if --pretty=tformat: <format> were given.

See the "PRETTY FORMATS" section for some additional details for each format. When =<format> part is omitted, it defaults to medium.

Note: you can specify the default pretty format in the repository configuration (see (1)).

- `--abbrev-commit`

Instead of showing the full 40-byte hexadecimal commit object name, show only a partial prefix. Non default number of digits can be specified with "--abbrev=<n>" (which also modifies diff output, if it is displayed).

This should make "--pretty=oneline" a whole lot more readable for people using 80-column terminals.

- `--no-abbrev-commit`

Show the full 40-byte hexadecimal commit object name. This negates --abbrev-commit and those options which imply it such as "--oneline". It also overrides the log.abbrevCommit variable.

- `--oneline`

This is a shorthand for "--pretty=oneline --abbrev-commit" used together.

- `--encoding=<encoding>`

The commit objects record the encoding used for the log message in their encoding header; this option can be used to tell the command to re-code the commit log message in the encoding preferred by the user. For non plumbing commands this defaults to UTF-8. Note that if an object claims to be encoded in X and we are outputting in X, we will output the object verbatim; this means that invalid sequences in the original commit may be copied to the output.

- `--notes[=<ref>]`

Show the notes (see (1)) that annotate the commit, when showing the commit log message. This is the default for git log, git show and git whatchanged commands when there is no --pretty, --format, or --oneline option given on the command line. By default, the notes shown are from the notes refs listed in the core.notesRef and notes.displayRef variables (or corresponding environment overrides). See (1) for more details.

With an optional <ref> argument, show this notes ref instead of the default notes ref(s). The ref is taken to be in refs/notes/ if it is not qualified.

Multiple --notes options can be combined to control which notes are being displayed. Examples: “--notes=foo” will show only notes from “refs/notes/foo”; “--notes=foo --notes” will show both notes from “refs/notes/foo” and from the default notes ref(s).

- `--no-notes`

Do not show notes. This negates the above --notes option, by resetting the list of notes refs from which notes are shown. Options are parsed in the order given on the command line, so e.g. “--notes=foo --no-notes --notes=bar” will only show notes from “refs/notes/bar”.

- `--show-notes[=<ref>], --[no-]standard-notes`

These options are deprecated. Use the above --notes/--no-notes options instead.

- `--show-signature`

Check the validity of a signed commit object by passing the signature to gpg --verify and show the output.

- `--no-commit-id`

git diff-tree outputs a line with the commit ID when applicable. This flag suppressed the commit ID output.

- `-c`

This flag changes the way a merge commit is displayed (which means it is useful only when the command is given one <tree-ish>, or --stdin). It shows the differences from each of the parents to the merge result simultaneously instead of showing pairwise diff between a parent and the result one at a time (which is what the *-m* option does). Furthermore, it lists only files which were modified from all parents.

- `--cc`

This flag changes the way a merge commit patch is displayed, in a similar way to the *-c* option. It implies the *-c* and *-p* options and further compresses the patch output by omitting uninteresting hunks whose the contents in the parents have only two variants and the merge result picks one of them without modification. When all hunks are uninteresting, the commit itself and the commit log message is not shown, just like in any other “empty diff” case.

- `--always`

Show the commit itself and the commit log message even if the diff itself is empty.

### PRETTY FORMATS

If the commit is a merge, and if the pretty-format is not oneline, email or raw, an additional line is inserted before the Author: line. This line begins with “Merge: ” and the shas1 of ancestral commits are printed, separated by spaces. Note that the listed commits may not necessarily be the list of the direct parent commits if you have limited your view of history: for example, if you are only interested in changes related to a certain directory or file.

There are several built-in formats, and you can define additional formats by setting a pretty.<name> config option to either another format name, or a format: string, as described below (see (1)). Here are the details of the built-in formats:

```
oneline
<sha1> <title line>

This is designed to be as compact as possible.
```

```
short
commit <sha1> Author: <author>
<title line>

medium
commit <sha1> Author: <author> Date: <author date>
<title line>
<full commit message>

full
commit <sha1> Author: <author> Commit: <committer>
<title line>
<full commit message>

fuller
commit <sha1> Author: <author> AuthorDate: <author date> Commit:
<committer> CommitDate: <committer date>
<title line>
<full commit message>
```

```
email
From <sha1> <date> From: <author> Date: <author date> Subject: [PATCH]
<title line>
<full commit message>

raw
The raw format shows the entire commit exactly as stored in the commit object.
Notably, the SHA-1s are displayed in full, regardless of whether --abbrev or --no-
```
