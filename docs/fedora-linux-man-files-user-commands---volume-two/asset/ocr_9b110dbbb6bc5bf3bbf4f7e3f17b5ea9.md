# OUTPUT

By default, any of the given pathnames which match an ignore pattern will be output, one per line. If no pattern matches a given path, nothing will be output for that path; this means that path will not be ignored.

If --verbose is specified, the output is a series of lines of the form:

```
<source> <COLON> <linenum> <COLON> <pattern> <HT> <pathname>
```

<pathname> is the path of a file being queried, <pattern> is the matching pattern, <source> is the pattern’s source file, and <linenum> is the line number of the pattern within that source. If the pattern contained a ! prefix or / suffix, it will be preserved in the output. <source> will be an absolute path when referring to the file configured by core.excludesFile, or relative to the repository root when referring to .git/info/exclude or a per-directory exclude file.

If -z is specified, the pathnames in the output are delimited by the null character; if --verbose is also specified then null characters are also used instead of colons and hard tabs:

```
<source> <NULL> <linenum> <NULL> <pattern> <NULL> <pathname> <NULL>
```

If -n or --non-matching are specified, non-matching pathnames will also be output, in which case all fields in each output record except for <pathname> will be empty. This can be useful when running non-interactively, so that files can be incrementally streamed to STDIN of a long-running check-ignore process, and for each of these files, STDOUT will indicate whether that file matched a pattern or not. (Without this option, it would be impossible to tell whether the absence of output for a given file meant that it didn’t match any pattern, or that the output hadn’t been generated yet.)

Buffering happens as documented under the GIT_FLUSH option in (1). The caller is responsible for avoiding deadlocks caused by overflowing an input buffer or reading from an empty output buffer.