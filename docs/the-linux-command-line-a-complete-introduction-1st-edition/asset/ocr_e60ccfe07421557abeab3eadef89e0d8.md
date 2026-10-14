This command lists all 100 directories and 2,600 files in *playground* (as well as *timestamp* and *playground* itself, for a total of 2,702) because none of them meets our definition of “good permissions.” With our knowledge of operators and actions, we can add actions to this command to apply new permissions to the files and directories in the playground:

```
[me@linuxbox ~]$ find playground \( -type f -not -perm 0600 -exec chmod 0600 '{ }' ';' \) -or \( -type d -not -perm 0700 -exec chmod 0700 '{ }' ';' \)
```

On a day-to-day basis, we might find it easier to issue two commands, one for the directories and one for the files, rather than this one large compound command, but it’s nice to know that we can do it this way. The important point here is to understand how operators and actions can be used together to perform useful tasks.

# Options

Finally, we have the options. The options are used to control the scope of a find search. They may be included with other tests and actions when constructing find expressions. Table 17-8 lists the most commonly used options.

Table 17-8: find Options

| Option | Description |
|---|---|
| -depth | Direct find to process a directory’s files before the directory itself. This option is automatically applied when the -delete action is specified. |
| -maxdepth levels | Set the maximum number of levels that find will descend into a directory tree when performing tests and actions. |
| -mindepth levels | Set the minimum number of levels that find will descend into a directory tree before applying tests and actions. |
| -mount | Direct find not to traverse directories that are mounted on other filesystems. |
| -noleaf | Direct find not to optimize its search based on the assumption that it is searching a Unix-like filesystem. This is needed when scanning DOS/Windows filesystems and CD-ROMs. |