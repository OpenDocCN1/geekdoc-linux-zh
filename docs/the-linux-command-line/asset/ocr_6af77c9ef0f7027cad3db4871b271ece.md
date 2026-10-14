The results contain all one hundred instances of file-B. Since we performed a touch on all the files in the playground named file-B after we updated timestamp, they are now “newer” than timestamp and thus can be identified with the -newer test.

Finally, let’s go back to the bad permissions test we performed earlier and apply it to playground:

```
[me@linuxbox ~]$ find playground \( -type f -not -perm 0600 \) -or \( -type d -not -perm 0700 \)
```

This command lists all one hundred directories and twenty-six hundred files in playground (as well as timestamp and playground itself, for a total of 2702) because none of them meets our definition of “good permissions.” With our knowledge of operators and actions, we can add actions to this command to apply new permissions to the files and directories in our playground:

```
[me@linuxbox ~]$ find playground \( -type f -not -perm 0600 -exec chmod 0600 '{}' ';' \) -or \( -type d -not -perm 0711 -exec chmod 0700 '{}' ';' \)
```

On a day-to-day basis, we might find it easier to issue two commands, one for the directories and one for the files, rather than this one large compound command, but it’s nice to know that we can do it this way. The important point here is to understand how the operators and actions can be used together to perform useful tasks.

# Options

Finally, we have the options. The options are used to control the scope of a find search. They may be included with other tests and actions when constructing find expressions. Here is a list of the most commonly used ones:

Table 18-7: find Options

| Option | Description |
|---|---|
| -depth | Direct find to process a directory's files before the directory itself. This option is automatically applied when the -delete action is specified. |
| -maxdepth levels | Set the maximum number of levels that find will descend into a directory tree when performing tests and |