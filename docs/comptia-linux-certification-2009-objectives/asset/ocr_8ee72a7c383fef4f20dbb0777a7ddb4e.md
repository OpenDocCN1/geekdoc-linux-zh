![](bbox=[0.11, 0.08, 0.67, 0.4])

# **Syntax**

The syntax of the find command is find `[options]` `[search locations]` `[search criteria]` `[actions]`.

# **find vs. locate commands**

The `locate` command searches a database and retrieves information on files present on your system. However, failure to keep this database updated may produce outdated results. The `find` command, on the other hand, performs a live search of the filesystem and may concentrate on a specific location. The `find` command may take more time to complete a search than the `locate` command.

# **Working of the find Command**

You can use the `find` command to search the entire directory structure for a file even if you remember a portion of the file name. One or more search paths can be designated and directory notations can be used as the search path. If no directory is specified, the `find` command uses the current working directory as the location to start the search. One or more criteria can be used to specify the conditions of a file or directory. In case of more than one search criterion, the file or directory must meet all the conditions specified before the results are displayed. The results displayed may be restricted to files users have permissions to access or execute. You can check the manual pages of the `find` command for more options.

# **Options for Files Found**

When the system finds a listing that meets your criteria, there are several actions that can be performed on the results. These options are outlined in the following table.

| **Option** | **Action Performed** |
| --- | --- |
| `-print` | Displays the location of the files found. |