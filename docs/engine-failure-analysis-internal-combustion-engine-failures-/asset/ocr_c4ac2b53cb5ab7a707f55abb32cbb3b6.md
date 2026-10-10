# OPTIONS (CONT.)

| **Use This Option** | **To Do This** |
| --- | --- |
| --mindepth *levels* | Begin processing tests and actions at the specified level below the current directory. Use an integer (a whole number) other than zero to specify *levels*. |
| --mount, --xdev | Do not search directories on other mounted filesystems. |
| --noleaf | Use this option when searching non-Unix file-systems, such as CD-ROMs or MS-DOS disks. |
| --version, --version | Display the version number. |

# TESTS

| **Use This Test** | **To Do This** |
| --- | --- |
| --amin *n* | Match files that were last accessed *n*minutes ago |
| --anewer *filename* | Match files that have been accessed since the specified *filename* was modified |
| --atime *n* | Match files that were last accessed *n* hours ago |
| --cmin *n* | Match files that were last changed *n*minutes ago |
| --cnewer *filename* | Match files that have been changed since the specified *filename* was modified. |
| --ctime *n* | Match files that were last changed *n* hours ago |
| --empty | Match files with 0 bytes of content. |
| --fstype *type* | Match files stored on the specified type of filesystem, such as msdos or vfat. |
| --gid *n* | Match files owned by the numeric group ID specified by *n*. |
| --ilname *shell pattern* | Match symbolic links with the specified *shell pattern*. Enclose the *shell pattern* in quotation marks. This search ignores case. |