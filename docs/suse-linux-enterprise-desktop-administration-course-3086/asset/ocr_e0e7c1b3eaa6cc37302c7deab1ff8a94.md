+   12. Copy the complete /bin directory to the home directory with the new directory named my_dir by entering

```
cp -r /bin ~/my_dir
```

+   13. Verify that the files were copied by entering

```
ls -l ~/my_dir
```

# Part II: Create New Directories

To create new directories, do the following:

+   1. Create a directory named new_dir inside the my_dir directory by entering

```
mkdir ~/my_dir/new_dir
```

+   2. Verify that the directory was created by entering

```
ls ~/my_dir
```

+   3. Create a gecko_dir/empty_dir directory by entering

```
mkdir -p ~/gecko_dir/empty_dir
```

+   4. Verify that gecko_dir was created by entering

```
ls
```

+   5. Verify that empty_dir was created by entering

```
ls gecko_dir
```

+   6. Close the terminal window.

# Part III: Delete Files and Directories

To delete files and directories, do the following:

+   1. Open a terminal window.

+   2. Try to remove the ~/gecko_dir directory by entering

```
rmdir gecko_dir
```

A message is displayed indicating that the directory cannot be removed because the
directory is not empty.

+   3. Remove the ~/gecko_dir/empty_dir directory by entering

```
rmdir gecko_dir/empty_dir
```

+   4. Verify that the /empty_dir directory has been removed by entering

```
ls gecko_dir
```

+   5. Remove the ~/gecko_dir directory by entering

```
rmdir gecko_dir
```