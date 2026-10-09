+   • ls a* a1 a12 a2
+   • ls [ab]? a1 a2 b1 b2
+   • ls [ab]* a1 a12 a2 b1 b12 b2
+   • ls [^ab]* c1 c12 c2
+   • ls ?[1-2] a1 a2 b1 b2 c1 c2
+   • ls ?[1-2]* a1 a12 a2 b1 b12 b2
+   c1 c12 c2

# Task 3:

Now, apply this shell globbing to find and execute a command on a certain set of files (copy and paste won't work for the below):

```
find . -name "c?" -execdir ls -l {} \
;
```

What this command is doing is searching in the current directory (recursively) for all files named "c?", which in this case matches c1 and c2. It then effectively executes `ls -l [file]` on each file found. The `!` syntax references the filename, while the escaped semicolon denotes the end of arguments to the `ls` command.

Experiment further with `find`:

+   • sudo find / -not -type l -perm -o+w
+   • sudo find / -perm -u+s -user root -type f

Both of the above commands are useful for security auditing purposes. The first one searches for (non-symlink) world-writable files. The second one searches for files which are "setuid root," or in other words, run with root permissions by a non-root user.

# Task 4:

Clean up:

+   • cd ..
+   • rm -r lab44

Notes:
Another useful command is `file`, which tells you a given file's type. Can you figure out how to use `file` in combination with find to locate all text files within your home directory?