# OPTIONS

<commit-ishi>...

Commit-ishi object names to describe.

--dirty[=<mark>]

Describe the working tree. It means describe HEAD and appends <mark> (-dirty by default) if the working tree is dirty.

--all

Instead of using only the annotated tags, use any ref found in refs/ namespace. This option enables matching any known branch, remote-tracking branch, or lightweight tag.

--tags

Instead of using only the annotated tags, use any tag found in refs/tags namespace. This option enables matching a lightweight (non-annotated) tag.

--contains

Instead of finding the tag that predates the commit, find the tag that comes after the commit, and thus contains it. Automatically implies --tags.

--abbrev=<n>

Instead of using the default 7 hexadecimal digits as the abbreviated object name, use <n> digits, or as many digits as needed to form a unique object name. An <n> of 0 will suppress long format, only showing the closest tag.

--candidates=<n>

Instead of considering only the 10 most recent tags as candidates to describe the input commit-ishi consider up to <n> candidates. Increasing <n> above 10 will take slightly longer but may produce a more accurate result. An <n> of 0 will cause only exact matches to be output.

--exact-match

Only output exact matches (a tag directly references the supplied commit). This is a synonym for --candidates=0.

--debug

Verbosely display information about the searching strategy being employed to standard error. The tag name will still be printed to standard out.

--long

Always output the long format (the tag, the number of commits and the abbreviated commit name) even when it matches a tag. This is useful when you want to see parts