# The Linux Cookbook: Tips and Techniques for Everyday Use:

+   • To compare the files `manuscript.old` and `manuscript.new`, type:

```
$ diff manuscript.old manuscript.new RET
```

The difference report is output to standard output; to save it to a file, redirect the output to the file to save to:

```
$ diff manuscript.old manuscript.new 62; manuscript.diff RET
```

In the preceding example, the difference report is saved to a file called `manuscript.diff`.

The difference report is meant to be used with commands such as patch, in order to apply the differences to a file. See Info file `diff.info`, node `Top`, for more information on diff and the format of its output.

To better see the difference between two files, use sdiff instead of diff; instead of giving a difference report, it outputs the files in two columns, side by side, separated by spaces. Lines that differ in the files are separated by `|`; lines that appear only in the first file end with a `<`, and lines that appear only in the second file are preceded with a `>`.

+   • To peruse the files `laurel` and `hardy` side by side on the screen, with any differences indicated between columns, type:

```
$ sdiff laurel hardy | less RET
```

To output the difference between three separate files, use diff3.

+   • To output a difference report for files `larry`, `curly`, and `moe`, and output it in a file called `stooges`, type:

```
$ diff3 larry curly moe 62; stooges RET
```

# 9.4.3 Patching a File with a Difference Report

To apply the differences in a difference report to the original file compared in the report, use patch. It takes as arguments the name of the file to be patched and the name of the difference report file (or "patchfile"). It then applies the changes specified in the patchfile to the original file. This is especially useful for distributing different versions of a file—small patchfiles may be sent across networks easier than large source files.

+   • To update the original file `manuscript.new` with the patchfile `manuscript.diff`, type: