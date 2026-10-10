
Any commits that have already been marked will not be exported again. If the backend uses a similar `--import-marks` file, this allows for incremental bidirectional exporting of the repository by keeping the marks the same across runs.

- `--fake-missing-tagger`
  Some old repositories have tags without a tagger. The fast-import protocol was pretty strict about that, and did not allow that. So fake a tagger to be able to fast-import the output.

- `--use-done-feature`
  Start the stream with a *feature done* stanza, and terminate it with a *done* command.

- `--no-data`
  Skip output of blob objects and instead refer to blobs via their original SHA-1 hash. This is useful when rewriting the directory structure or history of a repository without touching the contents of individual files. Note that the resulting stream can only be used by a repository which already contains the necessary objects.

- `--full-tree`
  This option will cause fast-export to issue a “deleteall” directive for each commit followed by a full list of all files in the commit (as opposed to just listing the files which are different from the commit’s first parent).

- `--anonymize`
  Anonymize the contents of the repository while still retaining the shape of the history and stored tree. See the section on ANONYMIZING below.

- `--refspec`
  Apply the specified refspec to each ref exported. Multiple of them can be specified.

- `[<git-rev-list-args>...]`
  A list of arguments, acceptable to *git rev-parse* and *git rev-list*, that specifies the specific objects and references to export. For example, *master~10..master* causes the current master reference to be exported along with all objects added since its 10th ancestor commit.

## EXAMPLES

```
$ git fast-export --all | (cd /empty/repository && git fast-import)`
```

This will export the whole repository and import it into the existing empty repository. Except for reencoding commits that are not in UTF-8, it would be a one-to-one mirror.

```
$ git fast-export master~5..master | sed "s|refs/heads/master|refs/heads/other|" | git fast-import
```

This makes a new branch called *other* from *master*~5..*master* (i.e. if *master* has linear history, it will take the last 5 commits).

Note that this assumes that none of the blobs and commit messages referenced by that revision range contains the string *refs/heads/master*.

# ANONYMIZING

If the `--anonymize` option is given, git will attempt to remove all identifying information from the repository while still retaining enough of the original tree and history patterns to reproduce some bugs. The goal is that a git bug which is found on a private repository will persist in the anonymized repository, and the latter can be shared with git developers to help solve the bug.

With this option, git will replace all refnames, paths, blob contents, commit and tag messages, names, and email addresses in the output with anonymized data. Two instances of the same string will be replaced equivalently (e.g., two commits with the same author will have the same anonymized author in the output, but bear no resemblance to the original author string). The relationship between commits, branches, and tags is retained, as well as the commit timestamps (but the commit messages and refnames bear no resemblance to the originals). The relative makeup of the tree is retained (e.g., if you have a root tree with 10 files and 3 trees, so will the output), but their names and the contents of the files will be replaced.

If you think you have found a git bug, you can start by exporting an anonymized stream of the whole repository:

```
$ git fast-export --anonymize --all >anon-stream
```

Then confirm that the bug persists in a repository created from that stream (many bugs will not, as they really do depend on the exact repository contents):

```
$ git init anon-repo
$ cd anon-repo
$ git fast-import <../anon-stream
$ ... test your bug...
```

If the anonymized repository shows the bug, it may be worth sharing anon-stream along with a regular bug report. Note that the anonymized stream compresses very well, so gzipping it is encouraged. If you want to examine the stream to see that it does not contain any private data, you can peruse it directly before sending. You may also want to try:

```
$ perl -pe 's/\d+/X/g' <anon-stream | sort -u | less
```

which shows all of the unique lines (with numbers converted to “X”), to collapse “User 0”, “User 1”, etc into “User X”). This produces a much smaller output, and it is usually easy to quickly confirm that there is no private data in the stream.

# LIMITATIONS

Since *git fast-import* cannot tag trees, you will not be able to export the linux.git repository completely, as it contains a tag referencing a tree instead of a commit.

# SEE ALSO

- git-fast-import(1)

# GIT-FAST-IMPORT

## NAME

git-fast-import - Backend for fast Git data importers

## SYNOPSIS

```
frontend | git fast-import [options]
```

## DESCRIPTION

This program is usually not what the end user wants to run directly. Most end users want to use one of the existing frontend programs, which parses a specific type of foreign source and feeds the contents stored there to *git fast-import*.

fast-import reads a mixed command/data stream from standard input and writes one or more packfiles directly into the current repository. When EOF is received on standard input, fast import writes out updated branch and tag refs, fully updating the current repository with the newly imported data.

The fast-import backend itself can import into an empty repository (one that has already been initialized by *git init*) or incrementally update an existing populated repository. Whether or not incremental imports are supported from a particular foreign source depends on the frontend program in use.

## OPTIONS

- `--force`
  Force updating modified existing branches, even if doing so would cause commits to be lost (as the new commit does not contain the old commit).

- `--quiet`
  Disable all non-fatal output, making fast-import silent when it is successful. This option disables the output shown by `--stats`.

- `--stats`
  Display some basic statistics about the objects fast-import has created, the packfiles they were stored into, and the memory used by fast-import during this run. Showing this output is currently the default, but can be disabled with `--quiet`.

### Options for Frontends

- `--cat-blob-fd=<fd>`
  Write responses to cat-blob and ls queries to the file descriptor `<fd>` instead of stdout. Allows progress output intended for the end-user to be separated from other output.

- `--date-format=<fmt>`
  Specify the type of dates the frontend will supply to fast-import within author, committer and tagger commands. See “Date Formats” below for details about which formats are supported, and their syntax.

- `--done`
  Terminate with error if there is no done command at the end of the stream. This option might be useful for detecting errors that cause the frontend to terminate before it has started to write a stream.

### Locations of Marks Files

- `--export-marks=<file>`
  Dumps the internal marks table to `<file>` when complete. Marks are written one per line as `.markid SHA-1`. Frontends can use this file to validate imports after they have been completed, or to save the marks table across incremental runs. As `<file>` is only opened and truncated at checkpoint (or completion) the same path can also be safely given to `--import-marks`.

- `--import-marks=<file>`
  Before processing any input, load the marks specified in `<file>`. The input file must exist, must be readable, and must use the same format as produced by `--export-marks`. Multiple options may be supplied to import more than one set of marks. If a
