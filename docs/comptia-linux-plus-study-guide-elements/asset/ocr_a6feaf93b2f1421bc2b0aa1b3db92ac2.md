# ## Removing Files

To delete a file, use the rm command, whose name is short for “remove.” Its syntax is simple:

```
rm [options] files
```

The rm command accepts many of the same options as cp or mv. Of those described in Table 2.2, --preserve and --update do not apply to rm, but all the others do. With rm, -r is synonymous with -R.

> By default, Linux doesn’t provide any sort of “trash-can” functionality for its rm command; once you’ve deleted a file with rm, it’s gone and cannot be recovered without retrieving it from a backup or performing low-level disk maintenance. Therefore, you should be cautious when using rm, especially as root. This is particularly true when you’re using the -R option—typing rm -R / will destroy an entire Linux installation! Many Linux GUI file managers implement trash-can functionality so that you can easily recover files moved to the trash (assuming you haven’t emptied the trash), so you may want to use a file manager for removing files.

# ## Touching Files

The touch command has two purposes: it can create a new empty file or it can adjust the last-modification and last-access times of an existing file. Using touch in the first way is helpful if you need to create an empty file for some reason (say, if another program expects a file to exist, but that file doesn’t need to have any content). Changing the file’s timestamp is useful if a program relies on this information and you need to change it. Programmers sometimes employ this feature to force development tools to recompile a source code file even if it hasn’t been modified since it was last compiled, for instance.

# ## Creating Links

The ln command creates hard links and soft links (aka symbolic links). Its syntax is similar to that of cp:

```
ln [options] source link
```

source is the original file, while link is the name of the link you want to create. This command supports options that have several effects, as summarized in Table 2.3.