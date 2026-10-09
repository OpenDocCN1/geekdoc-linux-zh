Your screen will be similar to Figure 6-20.

```
$ grep post-it -i *  
supply10:Post-It -- pads  
supply10:Post-It -- pop-up  
supply10:Post-It -- printed  
s
```

Figure 6-20 Case-insensitive grep Search

+   40. Robert asks you to append a note to the Post-It file, supply10, to remind him to reorder on February 27. You will use cat with a double redirect symbol, >>.  
+   a. Type cat >> supply10  
+   b. Press <Enter>  
+   c. Type Reorder 2/27  
+   d. Press <Enter> to move the cursor to the next line.  
+   e. Press <Enter> to add a blank line below the new text.  
+   f. Press <Ctrl-D>

+   41. Now look at the new version of supply10.  
+   a. Type cat supply10  
+   b. Press <Enter>

Your screen should look similar to Figure 6-21.

```
$ cat supply10  
Post-It notes -- pads  
Post-It notes -- pop-up  
Post-It notes -- printed  
Reorder 2/27  
s
```

Figure 6-21 supply10 With Appended Text