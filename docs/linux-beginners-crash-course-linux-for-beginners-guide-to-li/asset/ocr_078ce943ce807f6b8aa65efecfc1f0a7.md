# ## Removing non-empty directories

The command rm has a number of options that will change the way it works.
One very useful one is -r, meaning recursive, the same as in the command cp.
When you run rm with that -r option, you can remove directories that still
contain files and directories:

```
```
ls
backups foo3 fred
rmdir backups
rmdir: failed to remove 'backups': Directory not empty
rm backups
rm: cannot remove 'backups': Is a directory
rm -r backups
ls
foo3 fred
```
```

One good option to use with -r is -i, which means interactive. If you use this,
whenever you give the command to remove a directory or file, you will get a
prompt before each one is removed – this gives you the option of cancelling
if you’ve made a mistake.