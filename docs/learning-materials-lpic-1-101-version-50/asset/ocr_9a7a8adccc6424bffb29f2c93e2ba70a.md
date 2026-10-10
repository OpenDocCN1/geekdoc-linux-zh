# ## Summary

This lesson covers methods to run a program redirecting its standard communication channels. Linux processes use these standard channels as generic *file descriptors* to read and to write data, making it possible to arbitrarily change them to files or devices. The lesson goes through the following steps:

+   - What file descriptors are and the role they play in Linux.
+   - The standard communication channels of every process: *stdin*, *stdout* and *stderr*.
+   - How to correctly execute a command using data redirection, both for input and output.
+   - How to use *Here Documents* and *Here Strings* in input redirections.

The commands and procedures addressed were:

+   - Redirection operators: `>`, `<`, `>>`, `<<`, `<<<`.
+   - Commands `cat`, `set`, `uniq` and `wc`.