+   5. Make **list** executable by user, group, and others.
+   a.  Type **chmod a+X list**
+   b.  Press <Enter>

The default mode for a newly created file is usually

```
-rw-r--r--
```

For a shell script to run, the permissions must include read *and* execute; execute permission alone is not sufficient.

+   6. List your directory **scripts** to be certain that the file mode for **list** includes both read and execute permission. Your screen should look similar to Figure 9-2.

```
-rwxr-xr-x 1 ronasm 12  Fri Nov 17 9:12 list
$ |
```

![](bbox=[0.25, 0.43, 0.75, 0.45])

If user, group, and others do not have read permission for **list**, you must add that permission before someone in that user category (u, g, o) tries to run the script.

+   7. Run your new shell script, **list**.
+   a.  Type **list**
+   b.  Press <Enter>