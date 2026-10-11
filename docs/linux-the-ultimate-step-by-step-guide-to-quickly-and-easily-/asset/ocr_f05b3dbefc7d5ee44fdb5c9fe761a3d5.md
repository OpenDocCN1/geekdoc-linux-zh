This option is necessary with directories, regardless of whether the directory is empty. For instance, to copy the `some` directory structure to a new structure called `again`, we could type:

```
cp -r some again
```

Unlike with files, with which an existing destination would lead to an overwrite, if the target is an *existing directory*, the file or directory is copied *into* the target:

```
cp file1 again
```

This will create a new *copy of `file1`* and *place it inside the `again` directory*.

# Removing Files and Directories with “rm” and “rmdir”

To delete a file, you can use the `rm` command.

**Note:** Be extremely careful when using any destructive command like `rm`. There is no “undo” command for these actions so it is possible to accidentally destroy important files permanently.

To remove a regular file, just pass it to the `rm` command:

```
cd
```

```
rm file4
```

Likewise, to remove *empty* directories, we can use the `rmdir` command. This will only succeed if there is nothing in the directory in question. For instance, to remove the `example` directory within the `testing` directory, we can type:

```
rmdir testing/example
```

If you wish to remove a *non-empty* directory, you will have to use the `rm` command again. This time, you will have to pass the `-r` option, which removes all of the directory’s contents recursively, plus the directory itself.

For instance, to remove the `again` directory and everything within it, we can type:

```
rm -r again
```

Once again, it is worth reiterating that these are permanent actions. Be entirely sure that the command you typed is the one that you wish to execute.

# Editing Files