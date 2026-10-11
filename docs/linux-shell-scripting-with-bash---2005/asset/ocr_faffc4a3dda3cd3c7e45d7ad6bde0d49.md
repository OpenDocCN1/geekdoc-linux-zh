For easier reading, the `-L (label)` switch can be used to specify a title for the file, instead of reporting conflicts using the filename. This switch can be repeated three times for each of the three files.

For example, suppose there are three sets of orders for ice cream. The original set of orders (`file1.txt`) is as follows:

```
1 quart vanilla
2 quart chocolate
```

These orders have been modified by two people. The Barrie store now has (`file2.txt`) the following:

```
1 quart vanilla
1 quart strawberry
2 quart chocolate
```

And the Orillia (`file3.txt`) is as follows:

```
1 quart vanilla
2 quart chocolate
4 quart butter almond
```

The merge command reassembles the three files into one file.

```
$ merge -L "Barrie Store" -L "Original Orders" -L "Orillia Store" file2.txt
file1.txt file3.txt
```

`file1.txt file3.txt` will change `file2.txt` so that it contains:

```
1 quart vanilla
1 quart strawberry
2 quart chocolate
4 quart butter almond
```

However, if the *butter almond* and *strawberry* orders were both added as the third line, merge reports a conflict:

```
$ merge -L "Barrie Store" -L "Original Orders" -L "Orillia Store" file2.txt
file1.txt file3.txt
merge: warning: conflicts during merge
```

`file2.txt` will contain the details of the conflict:

```
««««« Barrie Store
1 quart strawberry
=======
4 quart butter almond
>>>>>>> Orillia Store
```

If there are no problems merging, merge returns a zero exit status.

The `-q (quiet)` switch suppresses conflict warnings. `-p (print)` writes the output to standard output instead of overwriting the original file. The `-3` switch reports conflicts in the `diff3 -A` format.