Let's back up a step and reconsider the **find** exercises. Suppose you don't know whether the filenames begin with an uppercase or a lowercase letter. You can use **find** with brackets to look for either instance.

The next seven exercises will take you on a three-part side trip.

+   29. You're going to rename **supply** as **Supply1**. (You're changing the first letter from lowercase to uppercase.) We can do it from the current directory, **practice**, but there's less room for error if you work in the directory in which the files reside.
+   a. Type `cd ../catalog`
+   b. Press <Enter>
+   c. Type `mv supply1 Supply1`
+   d. Press <Enter>

+   30. Now use **find** to locate files.
+   a. Type `find . -name 'supply*' -print`
+      Remember that the single dot is shorthand notation for the working directory.
+   b. Press <Enter>

Your screen will look similar to Figure 6-14.

```
$ find . -name 'supply*' -print
./supply10
./supply3
./supply7
./supply6
./supply9
$ |
```

![](bbox=[0.17, 0.73, 0.95, 0.8])

Linux is case sensitive. You instructed **find** to locate files beginning with a lowercase "s," which does not include **Supply**.