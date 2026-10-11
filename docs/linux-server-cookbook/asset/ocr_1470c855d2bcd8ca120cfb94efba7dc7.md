The command find searches for files, directories, or other objects in the system. This command, without options and arguments, will list all the elements recursively under the current directory. It forces to specify first the path and then the expressions to filter. There are multiple options and combinations, and the following table shows some of the most used:

| Option | Option description |
|---|---|
| -amin n | File was accessed less than, more than or exactly n minutes ago. |
| -atime n | File was last accessed less than, more than or exactly n*24 hours ago. |
| -cmin n | File was changed less than, more than or exactly n minutes ago. |
| -ctime n | File was last changed less than, more than or exactly n*24 hours ago. |
| -mmin n | File was modified less than, more than or exactly n minutes ago. |
| -mtime n | File was last modified less than, more than or exactly n*24 hours ago. |
| -name pattern | Filter the name of the file or directory with the pattern |
| -perm mode | Filter by the permission, useful to find vulnerable files |
| -size n[kMG] | File uses less than, more than or exactly n units. |
| -type c | Filter the type of the file, some of the options are are: |
|   | • b: block special |
|   | • c: character special |
|   | • d: directory |
|   | • f: file |
|   | • l: link |
| -user username/userid | File is owned by the user or user id specified. |
| -xdev | Don't descend directories on other filesystems. |

*Table 3.6: Common options for the command find*

The numeric n can be used with +n for greater than n, -n for less than n, and using n only is exactly that value. It is possible to perform different actions with the results using the options -delete, -exec commands as an example or formatting the output with options like -ls or -print0. The following figure shows how to filter files bigger than 1 megabyte: