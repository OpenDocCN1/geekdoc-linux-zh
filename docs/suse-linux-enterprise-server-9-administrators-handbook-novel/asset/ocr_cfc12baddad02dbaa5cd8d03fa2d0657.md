# **TABLE 6.4**  
Common chmod Settings (continued)

| COMMAND | TEXTUAL VALUE | MEANING |
|---|---|---|
| `chmod 500 directory` | `r-x --- ---` | To protect the owner from accidentally removing, renaming, or moving files from this private directory. |
| `chmod 600 file` | `rw- --- ---` | A file that can only be accessed and modified by the owner. A common setting for private files. |
| `chmod 644 file` | `rw- r-- r--` | A publicly readable file that can only be modified by the owner. |
| `chmod 660 file` | `rw- rw- ---` | The owner and members of the group owner have access, but not the world. A common setting for shared files. |
| `chmod 700 file` | `rwx --- ---` | Only the owner has full access to the file, and the file can be executed (such as a shell script). A common setting for a private shell script or program. |
| `chmod 701 directory` | `rwx --- --x` | Generally set on the “outgoing” directory on an FTP server where users can download a file only if they know the exact filename. |
| `chmod 703 directory` | `rwx --- -wx` | Generally set on the “incoming” directory on an FTP server where users can upload to files but cannot browse or download existing files. |
| `chmod 755 directory` | `rwx r-x r-x` | For files in a directory that should be readable and executable by others, but only changeable by the owner. |
| `chmod 775 file` | `rwx rwx r-x` | Standard file-sharing setting for a group. |
| `chmod 777 file` | `rwx rwx rwx` | Everybody can do everything to this file. |

# **CAUTION**

If you enter a number with fewer than four digits as an argument to chmod, omitted characters are replaced with zeros starting from the left. In other words, chmod 77 is the same as chmod 0077.