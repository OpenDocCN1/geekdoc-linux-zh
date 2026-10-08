# Working with the Shell

the pwd command, and then the mkdir command. Doing an ls will show you the contents. So, now that you know how to make a directory, you will need to know how to delete it from your Unix system as well.

# The rdir Command

The rmdir command will delete an empty directory. What this means that the directory you want to remove cannot contain any data within it.

To remove a directory, do the following:

+   - Decide which directory, or directories, you want out of your way.
- Issue the rmdir command as rmdir <directory>.

> Don't Forget! You Can Do Many At Once! Don't forget that you can remove multiple directories at one time. As with most file management commands, specify the directories in sequence and they will be removed. For example, if you wanted to remove "test" and "test1", the two directories could be removed with one issuance of the rmdir command. You could rmdir "test" and "test1" by typing rmdir test test1.

When you issue the rmdir command, you will remove the test directory you created before:

```
> rdir test
```

That's it! That was pretty easy to do. You should now be able to list the contents in your current directory and not see the test directory anywhere. It has been removed. If you had any problems, you may need to make the directory you want to remove empty In some cases, you must use rm * first to make the directory empty, and then you can delete it. As this is advanced syntax better covered in Lesson 13,