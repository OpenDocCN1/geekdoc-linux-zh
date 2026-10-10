+   9.  You cannot execute mycat against the `bash` profile file because you have removed the user's `x` permission. Linux responds with `bash: ./mycat: Permission denied.`

+   13. The simple `$ ls myscripts` works because the user still has read permission on the `myscripts` directory, and that is all that `ls` needs. `$ ls -l myscripts`, however, which requires both read and execute to work, does not work in this case because the `x` permission has been removed from that directory. Instead, you get `ls: myscripts/mycat: Permission denied` `ls: myscripts/mycat: Permission denied`

+   14. mycat will not execute because the `x` permission is needed to access any files, including executables, in a directory.

+   15. Both `x` and `w` permissions are needed to remove something from a directory.

# ## Chapter 7

+   1. The output of `1s` gives the names of the non-hidden files and subdirectories in only the current working directory. The output of `1s *` gives the names of the files and subdirectories in the current working directory and all subdirectories recursively down the directory tree from the current working directory. `1s *` does not display hidden files, but `1s -a` does. `1s -a` does not display the contents of subdirectories, but `1s *` does.

+   5. You might have, because the command is case sensitive. If you have files or directories beginning with upper-case letters from C through T, they are listed as well as all files and subdirectories recursively below them, no matter what quoting method is used.

+   6. All three methods work because the shell always disables wildcards, no matter what quoting method is used.

+   9. The output of `echo "* $n "ls" is" $n "ls"` because single quotes disable everything between them.
+   The output of `echo "* "$n "ls"` is `* hello filea` because double quotes disable only variable and command substitution variables.