| TABLE 3-5 (continued)\n| Single Letter | Full Word | Description |
| --- | --- | --- |
| -o | | In long listing not display owner names. |
| -r | --reverse | Reverse the sorting order when displaying files and directories. |
| -R | --recursive | List subdirectory contents recursively. |
| -s | --size | Print the block size of each file. |
| -S | --sort=size | Sort the output by file size. |
| -t | --sort=time | Sort the output by file modification time. |
| -u | | Display file last access time instead of last modification time. |
| -U | --sort=none | Don't sort the output listing. |
| -v | --sort=version | Sort the output by file version. |
| -x | | List entries by line instead of columns. |
| -X | --sort=extension | Sort the output by file extension. |

Besides the normal -l parameter output information, you'll see two additional numbers added to each line. The number in the listing is the file or directory inode number. The second number is the block size of the file. The third entry is a diagram of the type of file, along with the file's permissions. We'll delve into that in more detail in Chapter 6.

Following that, the next number is the number of hard links to the file (discussed later in the "Linking file" section), the owner of the file, the group the file belongs to, the size of the file (in bytes), a timestamp showing the last modification time by default, and finally, the actual filename.

# Filtering list output

As you've seen in the examples, by default the ls command lists all of the files in a directory. Sometimes this can be overkill, especially when you're looking for information on a single file.

Fortunately, the ls command also provide a way for us to define a filter on the command line. It uses the filter to determine which files or directories it should display in the output.

The filter works as a simple text-matching string. Include the filter after any command line parameters you want to use:

```
$ ls -l myprog
-rwxr-xr-- 1 rich 30 2007-08-23 21:42 myprog $
```