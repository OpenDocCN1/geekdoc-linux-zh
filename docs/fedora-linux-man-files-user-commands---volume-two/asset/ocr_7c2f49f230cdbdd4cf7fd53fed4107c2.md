When giving multiple pattern expressions combined with —or, this flag is specified to limit the match to files that have lines to match all of them.

-q, —quiet

Do not output matched lines; instead, exit with status 0 when there is a match and with non-zero status when isn’t.

<tree>...

Instead of searching tracked files in the working tree, search blobs in the given trees.

—

Signals the end of options; the rest of the parameters are <pathspec> limiters.

<pathspec>...

If given, limit the search to paths matching at least one pattern. Both leading paths match and (7) patterns are supported.