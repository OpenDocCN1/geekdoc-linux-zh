# ## Background Material

ELF (Executable and Link Format) is a file format for executable files. It is widely used in the UNIX world.

You also discover that `/usr/bin/locate` is dynamically linked, and that it contains no symbol table or debugging information— it is stripped.

The following is another example:

```
```
$ file /opt/kde/share/wallpapers/parrots.jpg
/opt/kde/share/wallpapers/parrots.jpg: JPEG image data, JFIF standard
```
```

`file` makes surprisingly good guesses about most file types. If it cannot identify a file type, it simply prints ASCII text or data.

`file` has built-in algorithms for some types of files, but it also makes use of two files for user-supplied hints. `/usr/share/misc/magic` and `/etc/magic` contain hints in a special format that `file` can use to identify files. You can find out how they work by reading the manual pages `find(1)` and `magic(5)`.

# # Looking at Part of a File: head and tail

`head` and `tail` are very simple commands. They send the first or last few lines of a file to standard output. The following explains how to use them:

+   - `head -n file` sends the first `n lines` of `file` to standard output. If `-n` is omitted, 10 lines are outputted. If `file` is omitted, `head` sends the first `n` lines of its standard input to standard output.
+   - `tail -n file` sends the last `n lines` of `file` to standard output. If `-n` is omitted, 10 lines are outputted. If `file` is omitted, standard input is used.
+   - `tail +n file` sends the last lines of `file` starting with line `n` to standard output. For example, to see all but the first line of a file, use
+   `$ tail +2 file`
+   - `tail -f file` causes `tail` to loop forever, waiting for the file to grow. If the file grows, the additional lines are sent to standard output. This is useful if you have a process writing to a file and you want to monitor the progress of the file.

Both `head` and `tail` can take more than one `file` argument; in that case, they print a one-line header before the file contents to identify which file is being viewed.