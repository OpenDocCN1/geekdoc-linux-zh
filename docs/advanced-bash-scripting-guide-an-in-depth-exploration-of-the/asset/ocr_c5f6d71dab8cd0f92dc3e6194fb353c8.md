# Advanced Bash-Scripting Guide

```
'dig,' version 9.x.x (dig $HOSTNAME, see first line of output)
A version of dig which supports the +short options.
See: dig-wrappers.bash for details.
```

# Optional Prerequisites

'named,' a local DNS caching program. Any flavor will do.
To twice: dig $HOSTNAME
Check near bottom of output for: SERVER: 127.0.0.1#53
That means you have one running.

# Optional Graphics Support

'date,' a standard *nix thing. (date -R)

dot program to convert graphic description file to a
diagram. (dot -V)
A part of the Graph-Viz set of programs.
See: [http://www.research.att.com/sw/tools/graphviz/|GraphViz]

'dotry,' a visual editor for graphic description files.
Also a part of the Graph-Viz set of programs.

# Quick Start

In the same directory as the is_spammer.bash script;
Do: ./is_spammer.bash

# Usage Details

+   1. Blacklist server choices.

+   (a) To use default, built-in list: Do. nothing.
(b) To use your own list:

+   i. Create a file with a single Blacklist server
domain name per line.
ii. Provide that filename as the last argument to
the script.
(C) To use a single Blacklist server: Last argument
to the script.
(d) To disable Blacklist lookups:
i. Create an empty file (touch spammer.null)
Your choice of filename.
ii. Provide the filename of that empty file as the
last argument to the script.

+   2. Search depth limit.

+   (a) To use the default value of 2: Do nothing.

# Appendix A. Contributed Scripts