```
% mv New.Sample.Directory dave
mv: New.Sample.Directory: rename: Not a directory
```

The reverse situation works fine because the file is moved into the directory as expected. This is the subtlety of using the mv command to rename files.

+   4. If you assign a new directory a name that belongs to an existing directory, some versions of mv will happily overwrite the existing directory and name the new one as requested:

Click here to view code image

```
% mkdir testdir
% mv New.Sample.Directory testdir
```

Being able to rename files is another important part of building a useful Unix virtual file cabinet for you. Some major dangers are involved, however, so tread carefully and always use ls in conjunction with cp and mv to ensure that in the process you don’t overwrite or replace an existing file.

# Task 6.5: Removing Directories with rmdir

Now that you can create directories with the mkdir command, it’s time to learn how to remove directories using the rmdir command.

+   1. With rmdir, you can remove any directory for which you have appropriate permissions:

```
% mkdir test
% ls -l test
total 0
% rmdir test
```

Note that the output of ls shows that there are no files in the test directory.

+   2. By default, the rmdir command removes only directories that are empty:

Click here to view code image

```
% mkdir test
% touch test/sample.file
% ls -l test
total 0
-rw-rw-- 1 taylor 0 Nov 5 14:00 sample.file
% rmdir test
rmdir: test: Directory not empty
```

To remove a directory, you must first remove all files therein using the rm command. In this example, test still has files in it. Note that some versions of rmdir offer the -p flag, which will recursively remove all directories and subdirectories from right to left until it encounters a non-empty directory. Other versions include the -f flag, which will let you forcibly remove any files or subdirectories contained within the specified directory. As you imagine, rmdir -f / could destroy your system, so be careful!

+   3. Permissions are important, too. Consider what happens when I try to remove a directory that I don’t have permission to touch: