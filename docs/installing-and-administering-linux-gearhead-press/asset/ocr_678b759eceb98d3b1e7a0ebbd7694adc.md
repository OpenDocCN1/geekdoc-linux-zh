```
./admin/phones$/RfI Tel3
./admin/Repts-ac_pay
./admin/Repts-rec
./Req-X1
./Req-X2
./Req-X3
```

She now sees that she saved her `Repts-ac_pay` file in her `admin` subdirectory, but she notices that a high proportion of her filenames seem to begin with R. "Huh?" she thinks. "If I ever get any spare time, I suppose I'll have to do something about that, too."

# The find Command with
the -links Option

In this section, we discuss the use of the `-links` option with `find`. There are two reasons to use this command combination:

+   ■ If you can have the same file referenced by two separate names, the only way you can tell whether they are indeed the same file is by examining the inode number. If the inode numbers are identical, they are the same file.
+   ■ More importantly, for security reasons you do not want outsiders linking to insider programs or files. You must have a way of seeing and confirming where all links are pointing to evaluate whether they are necessary and legitimate. Therefore, it is important to conduct a `find -links` check periodically to search for such potential infiltration.

The syntax is as follows (and here, we use "line continuation" from Chapter 7, "Shell Basics," to split and then continue the commands):

```
$ find directory(ies) -type [options] -links +[options]\<Enter>
> | xargs ls -li<Enter>
```

Example 9.6 is typical of a `find -links` check. Note that you should be certain to perform `-links` checks on only *files* because directories by their nature have at least two links (their own and their link with the parent directory). Note that the linked files' inode numbers, link counts, and file sizes are the same. The only difference among the three is their respective filenames. Rest assured that they all refer to the same file, regardless of their names.