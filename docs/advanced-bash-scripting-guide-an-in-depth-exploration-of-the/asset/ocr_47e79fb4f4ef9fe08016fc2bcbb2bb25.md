# Advanced Bash-Scripting Guide

+   (b) To set a different limit:
A limit of 0 means: no limit.

+   i. export SPAMMER_LIMIT=1
or whatever limit you want.

+   ii. OR provide the desired limit as the first
argument to the script.

+   3. Optional execution trace log.

+   (a) To use the default setting of no log output: Do Nothing.

+   (b) To write an execution trace log:
export SPAMMER_TRACE=spammer.log
or whatever filename you want.

+   4. Optional graph description file.

+   (a) To use the default setting of no graph file: Do Nothing.

+   (b) To write a Graph-Vis graph description file:
export SPAMMER_DATA=spammer.dot
or whatever filename you want.

+   5. Where to start the search.

+   (a) Starting with a single domain name:

+   i. Without a command-line search limit: First
argument to script.

+   ii. With a command-line search limit: Second
argument to script.

+   (b) Starting with a single IP address:

+   i. Without a command-line search limit: First
argument to script.

+   ii. With a command-line search limit: Second
argument to script.

+   (c) Starting with (mixed) multiple name(s) and/or address(es):
Create a file with one name or address per line.
Your choice of filename.

+   i. Without a command-line search limit: Filename as
first argument to script.

+   ii. With a command-line search limit: Filename as
second argument to script.

+   6. What to do with the display output.

+   (a) To display output on screen: Redirect stdout to a filename.

+   (b) To save display output to a file: Redirect stdout to /dev/null.

+   (c) To discard display output: Redirect stdout to /dev/null.