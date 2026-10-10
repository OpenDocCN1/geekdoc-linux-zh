# umask

**umask [ option ] [ nnn ]**

Displays or sets the *file creation mask*, the permissions that are automatically applied to new files. To determine the file creation mask, you specify a three-digit number, such as 022. This number is subtracted from the highest possible permission level, 777. A umask of 022 generates a permission level of 755, which is equivalent to symbolic mode u=rwX, g=rX, o=rX.

OPTION

| Use This Option | To Do This |
| :-------------- | :--------- |
| -S | Display the current file permission list using the symbolic mode |

# undelele

**undelele [ option ] [ filename ]**

Restores files deleted with the **safedele** command. Undeleted files are returned to their original location, and all original attributes (including permissions and timestamps) are restored. To specify the filename, you can use wildcards (* and ?). When the list of deleted files appears, you can use the commands (For the **undelele** commands, see the Commands table in this section). If this utility is not included in your Linux distribution, you can obtain the source code from [http://meta.lab.unc.edu/pub/Linux/utils/shell1/](http://meta.lab.unc.edu/pub/linux/utils/shell1/).

See also **safedele**.

OPTIONS

| Use This Option | To Do This |
| :-------------- | :--------- |
| -i, -info | Display information about the file. |
| -l, -list | Display a list of **safedeleted** files that can be restored. |