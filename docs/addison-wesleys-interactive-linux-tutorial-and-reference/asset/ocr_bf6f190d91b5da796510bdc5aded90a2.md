```
```text
-rwxr-xr-x 1 rongm 15 Sep 19 8:12 list
-rwxr-xr-x 1 rongm 78 Sep 19 8:15 list2
-rwxr-xr-x 1 rongm 154 Sep 19 8:21 ren
-rw-r-- 1 rongm 22 Sep 19 8:25 thisfile
```
```

Figure 9-6 List of Files in the Directory scripts

+   - 17. Run the script `ren`. Change the name of that new file from `thisfile` to `thatfile`.
+       18. List the directory `scripts` to be certain that the filename has been changed.

For the final exercise in this module, you will create a script that adds a tiny bit of automation to `grep`. To put the script to use, you will use the supply files you created as Roberr's intern. Those files are in the directory `catalog`. Figure 9-7 displays the directory structure you have created so far.

```
```text
/home/userid
    /practice
        /backup
        /catalog
        /dir1
        /dir2
        /scripts
```
```

Figure 9-7 Directory Structure You have Created

+   - 19. Change to the directory `catalog`. Use the double dot notation (..) to make this change.
+       20. Create a script that uses `grep`. Call the script `srch`.
+           a. Type `cat > srch`
+           b. Press <Enter>
+           c. Type `echo -n "What do you want to find? "`
+           d. Press <Enter>