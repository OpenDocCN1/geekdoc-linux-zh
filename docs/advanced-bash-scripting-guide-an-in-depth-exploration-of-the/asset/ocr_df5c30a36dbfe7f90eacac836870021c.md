# Advanced Bash-Scripting Guide

The -s option squeezes multiple consecutive blank lines into a single blank line.

See Example 16-28 and Example 16-24.

> In a pipe, it may be more efficient to redirect the stdin to a file, rather than to cat the file.

| cat filename | tr a-z A-Z |
| tr a-z A-Z < filename # Same effect, starts one less process
# and also dispenses with the pipe. |

tac, is the inverse of cat, listing a file backwards from its end.

reverses each line of a file, and outputs to stdout. This does not have the same effect as tac, as it preserves the order of the lines, but flips each one around (mirror image).

```
bash$ tac file1.txt
This is line 1.
This is line 2.

bash$ tac file1.txt
This is line 2.
This is line 1.

bash$ rev file1.txt
1 enil si siHT
2 enil si siHT
```

This is the file command. cp file1 file2 copies file to file2, overwriting file2 if it already exists see Example 16-6.

+   Particularly useful are the -a archive flag (for copying any directory tree),
-update flag which prevents overwriting identically-named newer files), and
-r and -R recursive flags.

```
cp -u source_dir/* dest_dir
# "Synchronization" dest_dir to source_dir
# by copying over newer and not previously existing files.
```

This is the move command. It is equivalent to a combination of cp and rm. It may be used to move multiple files to a directory, or even to rename a directory. For some examples of mv in a script, see Example 10-11 and Example A-2.

> When used in a non-interactive script, mv takes the -f (force) option to bypass user input.

When a directory is moved to a preexisting directory, it becomes a subid of the destination directory.

```
bash mv source_directory target_directory
```