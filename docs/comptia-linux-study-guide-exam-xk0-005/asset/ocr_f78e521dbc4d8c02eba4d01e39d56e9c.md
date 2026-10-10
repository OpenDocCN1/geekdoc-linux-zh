# TABLE 3.8 The locate command’s commonly used options

| Short | Long | Description |
| :--- | :--- | :--- |
| -A | --all | Display filenames that match all the patterns, instead of displaying files that match only one pattern in the pattern list. |
| -b | --basename | Display only file names that match the pattern and do not include any directory names that match the pattern. |
| -c | --count | Display only the number of files whose name matches the pattern instead of displaying file names. |
| -i | --ignore-case | Ignore case in the pattern for matching filenames. |
| -q | --quiet | Do not display any error messages, such as permission denied, when processing. |
| -r | --regexp R | Use the regular expression, R, instead of the pattern list to match filenames. |
| -w | --wholename | Display filenames that match the pattern and include any directory names that match the pattern. This is default behavior. |

To find a file with the `locate` command, just enter **locate** followed by the filename. If the file is on your system and you have permission to view it, the `locate` utility will display the file’s directory path and name. An example of this is shown in Listing 3.39.

```
**Listing 3.39:** Using the `locate` command to find a file
$ locate Project42.txt
/home/Christine/Answers/Project42.txt
$
```

Using the `locate` command *PATTERN* can be a little tricky, due to default pattern *file globbing*. File globbing occurs when you use wildcards, such as an asterisk (*) or a question mark (?), added to a filename argument in a command, and the filename is expanded into multiple names. For example, `passw*d` could be expanded into the filename `password` or `passwd`.

If you don’t enter any wildcards into your pattern, the `locate` command, by default, adds wildcards to the pattern. So if you enter the pattern, **passwd**, it is automatically turned into **\*passwd\***. Thus, if you just want to search for the base name `passwd`, with no file