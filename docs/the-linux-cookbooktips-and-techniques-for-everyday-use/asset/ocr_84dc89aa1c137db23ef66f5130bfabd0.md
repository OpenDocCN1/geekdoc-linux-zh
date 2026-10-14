# The Linux Cookbook: Tips and Techniques for Everyday Use:

files, type:

```
$ ls -F RET
repeat* test1  test2  words/
$
```

In this example, the current directory contains an executable file named `repeat`, a directory named `words`, and some other files named `test1` and `test2`.

Another way to list the contents of directories—and one I use all the time, when I'm in X and when I also want to look at image files in those directories—is to use Mozilla or some other Web browser as a local file browser. Use the prefix [16]file:// to view local files. Alone, it opens a directory listing of the root directory; file://home/joe opens a directory listing of user joe's home directory, file://usr/local/src opens the local source code directory, and so on. Directory listings will be rendered in HTML on the fly in almost all browsers, so you can click on subdirectories to traverse to them, and click on files to open them in the browser.

Yet another way to list the contents of directories is to use a "file manager" tool, of which there are at least a few on Linux; the most popular of these is probably the "Midnight Commander," or mc.

The following subsections describe some commonly used options for controlling which files ls lists and what information about those files ls outputs. It is one of the most often used file commands on Unix-like systems.

+   6.3.1 Listing File Attributes
+   6.3.2 Listing Directories Recursively
+   6.3.3 Listing Newest Files First
+   6.3.4 Listing Hidden Files
+   6.3.5 Listing Directories in Color
+   6.3.6 Listing Directory Tree Graphs
+   6.3.7 Additional Directory Listing Options

+   Listing file attributes.
+   Listing directories and their subdirectories.
+   Listing newest files first.
+   Listing hidden or special files.
+   Directory listings in color.
+   Listing an entire directory tree.
+   Popular options for the ls command.

# 6.3.1 Listing File Attributes

Use ls with the `-l` ("long") option to output a more extensive directory listing—one that contains each file's size in bytes, last modification time, file type, and ownership and permissions (see section File Ownership).

+   To output a verbose listing of the `/usr/doc/bash` directory, type: