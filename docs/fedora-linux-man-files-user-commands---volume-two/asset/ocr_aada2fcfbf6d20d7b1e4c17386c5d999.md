# OPTIONS

—follow
Continue listing the history of a file beyond renames (works only for a single file).

—no-decorate, —decorate[=short|full|no]
Print out the ref names of any commits that are shown. If *short* is specified, the ref name prefixes *refs/heads/*, *refs/tags/* and *refs/remotes/* will not be printed. If *full* is specified, the full ref name (including prefix) will be printed. The default option is *short*.

—source
Print out the ref name given on the command line by which each commit was reached.

—use-mailmap
Use mailmap file to map author and committer names and email addresses to canonical real names and email addresses. See (1).

—full-diff
Without this flag, git log -p `<path>...` shows commits that touch the specified paths, and diffs about the same specified paths. With this, the full diff is shown for commits that touch the specified paths; this means that “`<path>...`” limits only commits, and doesn’t limit diff for those commits.

Note that this affects all diff-based output types, e.g. those produced by --stat, etc.

—log-size
Include a line “log size `<number>`” in the output for each commit, where `<number>` is the length of that commit’s message in bytes. Intended to speed up tools that read log messages from git log output by allowing them to allocate space in advance.

-L `<start>,<end>:<file>` , -L `<funcname>:<file>`
Trace the evolution of the line range given by “`<start>,<end>`” (or the function name regex `<funcname>`) within the `<file>`. You may not give any pathspec limiters. This is currently limited to a walk starting from a single revision, i.e., you may only give zero or one positive revision arguments. You can specify this option more than once.
`<start>` and `<end>` can take one of these forms:
number
If `<start>` or `<end>` is a number, it specifies an absolute line number (lines count from 1).

/regex/