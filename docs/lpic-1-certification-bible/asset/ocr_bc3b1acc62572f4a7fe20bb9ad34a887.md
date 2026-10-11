A variety of options can be used to specify the information displayed with the file listings. Table 6-2 covers the information listing options used with the `ls` command.

| **Table 6-2**
**Information Listing Options Used with ls** | |
| :--- | :--- |
| **Option** | **Use** |
| `-G` | Specifies that group information is not to be displayed. |
| `-i` | Displays the inode number. |
| `-l` | Displays file type, permissions, hard link count, file owner, group owner, and modification time. |
| `-O` | Displays the same information as the `-l` option except group information is excluded. |
| `-s` | Displays the file size in 1024-byte blocks. |

The `ls` command also uses options to order the output that is displayed. These options are shown in Table 6-3.

| **Table 6-3**
**Output Ordering Options Used with ls** | |
| :--- | :--- |
| **Option** | **Use** |
| `-c` | Displays output according to the status change time or time of the inode. |
| `-f` | Displays output in the order which they were saved in the directory. |
| `-r` | Displays output in reverse order. |
| `-S` | Displays files according to size from largest to smallest. |
| `-t` | Displays files by modification time beginning with most recent. |
| `-u` | Displays files by access time beginning with most recent. |

The output produced with the `ls` command can also be controlled with another set of options. The options shown in Table 6-4 control the appearance of the output produced.