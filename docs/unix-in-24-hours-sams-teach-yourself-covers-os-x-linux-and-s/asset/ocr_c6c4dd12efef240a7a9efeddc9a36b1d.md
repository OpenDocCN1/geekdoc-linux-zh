In this case, the shell matches all files that start with *a*, *b*, *k*, *o*, *s*, or *t*. This notation is still a bit clunky and would be even more so if more files were involved.

+   7. You can specify a range of characters by putting a hyphen in the middle:

![](bbox=[0.059, 0.143, 0.812, 0.325])

In this example, the shell will match any file that begins with a lowercase letter from *a* to *z*, as specified.

+   8. The combination of character ranges, single-character wildcards, and multicharacter wildcards can be tremendously helpful. If I move to another directory, I can easily search for all files that contain a single digit, a dot, or an underscore in the name:

![](bbox=[0.059, 0.452, 0.907, 0.542])

I think that the best way to learn about pervasive features of Unix such as shell filename wildcards is to use them. As you’ve no doubt noticed so far in this book, examples build on earlier information. This will continue to be the case, and the wildcard notations shown here are used again and again to specify groups of files or directories.

If you want to experiment with filename wildcards, you can most easily use the `echo` command because it safely prints the expanded version of any pattern you specify without otherwise doing anything with those files. Lots of Unix experts use echo to develop and fine-tune a pattern and then use the pattern with a different command.

# Task 8.5: Searching Files with grep

Two commonly used commands are important stepping stones in becoming a power user comfortable with the capabilities of the system: the `ls` command and the `grep` command. We’ve already looked at the `ls` command, so let’s turn our attention to the oddly named `grep` command, which makes it easy to find files that contain specified text patterns.

The `grep` command not only has a ton of command options but has two variations in Unix systems, too. These variations are `egrep`, for specifying more complex patterns (regular expressions), and `fgrep`, for using file-based lists of words as search patterns.