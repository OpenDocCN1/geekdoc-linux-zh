linux.txt
114684 4 -rw-rw-r- 1 kburtch kburtch 592 May 17 14:41 ./advocacy/o
ld_orders.txt

The `-printf` switch makes `find` act like a searching version of the `stat`/`fstat` command. The `%` format codes indicate what kind of information about the file to print. Many of these provide the same functions as `stat`/`fstat`, but use a different code.

+   - `%a` — File's last access time in the format returned by the `C` `ctime` function.
+   - `%c` — File's last status change time in the format returned by the `C` `ctime` function.
+   - `%f` — File's name with any leading directories removed (only the last element).
+   - `%g` — File's group name, or numeric group ID if the group has no name.
+   - `%h` — Leading directories of file's name (all but the last element).
+   - `%i` — File's inode number (in decimal).
+   - `%m` — File's permission bits (in octal).
+   - `%p` — File's pathname.
+   - `%P` — File's pathname with the name of the command line argument under which it was found removed.
+   - `%s` — File's size in bytes.
+   - `%t` — File's last modification time in the format returned by the `C` `ctime` function.
+   - `%u` — File's username, or numeric user ID if the user has no name.

A complete list appears in the reference section.

The time codes also differ from `stat`/`fstat`: `stat`/`fstat` remembers the last type of time selected, whereas `find` requires the type of time for each time element printed.

```
`$ find . -type f -name "*.txt" -printf "%f access time is %a\n"`
`orders.txt access time is Thu May 17 16:47:08 2001`
`linux.txt access time is Thu May 17 16:47:08 2001`
`old_orders.txt access time is Thu May 17 16:47:08 2001`
`$ find . -type f -name "*.txt" -printf "%f modified time is %` \
`hours%minutes is %H:%M\n"`
`orders.txt modified time as hours:minutes is 14:41`
`linux.txt modified time as hours:minutes is 14:41`
`old_orders.txt modified time as hours:minutes is 14:41`
```

A complete list of `find` switches appears in the reference section.

# # Sorting

The Linux `sort` command sorts a file or a set of files. A file can be named explicitly or redirected to sort on standard input. The switches for sort are completely different from commands such as `grep` or `cut`. `sort` is one of the last commands to support long versions of switches; as a result, the short switches are used here. Even so, the switches for common options are not the same as other Linux commands.