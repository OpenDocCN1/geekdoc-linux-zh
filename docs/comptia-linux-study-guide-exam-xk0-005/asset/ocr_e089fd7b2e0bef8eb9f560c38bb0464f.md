/usr/bin/passwd  
/usr/share/X11/xkb/symbols/group  
/usr/share/bash-completion/completions/passwd  
$ 

Another problem you can run into deals with newly created or downloaded files. The `locate` utility is really searching the `mlocate.db` database as opposed to searching the virtual directory structure. This database is typically updated only one time per day via a `cron` job. Therefore, if the file is newly created, `locate` won't find it.

The `mlocate.db` database is updated via the `updatedb` utility. You can run it manually using super user privileges if you need to find a newly created or downloaded file. Be aware that it may take a while to run.

# # Using Intricate Pinpoint Commands

While using simple commands to locate files is useful, they don't work in situations where you need to find files based on things such as metadata. Thankfully, there are more complex commands that can help.

The `find` command is flexible. It allows you to locate files based on data, such as who owns the file, when the file was last modified, permission set on the file, and so on. The basic command syntax is:

```
find [PATH...] [OPTION] [EXPRESSION]
```

The `PATH` argument is a starting point directory, because you designate a starting point in a directory tree and `find` will search through that directory and all its subdirectories (recursively) for the file or files you seek. You can use a single period (.) to designate your present working directory as the starting point directory.

![](bbox=[0.15, 0.8, 0.27, 0.86])

There are also options for the `find` command itself that handle such items as following or not following links and debugging. In addition, you can have a file deleted or a command executed if a particular file is located. See the `find` utility's man page for more information on these features.

The `EXPRESSION` command argument and its preceding `OPTION` control what type of metadata filters are applied to the search as well as any settings that may limit the search. Table 3.9 shows the more commonly used `OPTION` and `EXPRESSION` combinations.

The `find` utility has many features. Examples help clarify the use of this command. Listing 3.42 provides a few.