# ANCHORING INCLUDE/EXCLUDE PATTERNS

As ntioned earlier, global include/exclude patterns are anchored at the “root of the transfer” (as opposed to per-directory patterns, which are anchored at the rge-file’s directory). If you think of the transfer as a subtree of nas that are being sent from sender to receiver, the transfer-root is where the tree starts to be duplicated in the destination directory. This root governs where patterns that start with a / match.

Because the matching is relative to the transfer-root, changing the trailing slash on a source path or changing your use of the —relative option affects the path you need to use in your matching (in addition to changing how ch of the file tree is duplicated on the destination host). The following examples demonstrate this.

Let’s say that we want to match two source files, one with an absolute path of “/ho//foo/bar”, and one with a path of “/ho//you/bar/baz”. Here is how the various command choices differ for a 2-source transfer:

Example cmd: rsync -a /ho/ /ho/you /dest +/- pattern: //foo/bar +/- pattern: /you/bar/baz Target file: /dest//foo/bar Target file: /dest/you/bar/baz

Example cmd: rsync -a /ho// /ho/you/ /dest +/- pattern: /foo/bar (note missing “”) +/- pattern: /bar/baz (note missing “you”) Target file: /dest/foo/bar Target file: /dest/bar/baz

Example cmd: rsync -a —relative /ho// /ho/you /dest +/- pattern: /ho//foo/bar (note full path) +/- pattern: /ho/you/bar/baz (ditto) Target file: /dest/ho//foo/bar Target file: /dest/ho/you/bar/baz

Example cmd: cd /ho; rsync -a —relative /foo you/ /dest +/- pattern: //foo/bar (starts at specified path) +/- pattern: /you/bar/baz (ditto) Target file: /dest//foo/bar Target file: /dest/you/bar/baz

The easiest way to see what na you should filter is to just look at the output when using —verbose and put a / in front of the na (use the —dry-run option if you’re not yet ready to copy any files).