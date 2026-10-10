# EXAMPLE

| This Command | Does the Following |
|---|---|
| `rmdir /home/suzanne/junk` | Removes the specified directory if it is empty. |

# safedlete

**safedlete [ option ] file**

Deletes the specified file to the safedlete directory, where it is retained for a specified interval before being deleted permanently. You can use a shell pattern to specify the filename (see the section "Shell Patterns" in Chapter 4). You can use alias (see Chapter 3) so that safedlete is used instead of rm. To recover a deleted file, use undelete. If this utility is not included in your Linux distribution, you can obtain the source code from `http://metalab.unc.edu/pub/Linux/utils/shell/`.

See also undelete.

# OPTIONS

| Use This Option | To Do This |
|---|---|
| `-i, -interactive` | Prompt the user before deleting a file |
| `-v, -verbose` | Print the name of each file before deleting it |
| `-f, -force` | Ignore nonexistent files and do not prompt the user |
| `-r, -R, -recursive` | Delete all the files in the current directory and all of its associated subdirectories |
| `--help` | Display command options |
| `--version` | Display the command version |

# EXAMPLES

| This Command | Does the Following |
|---|---|
| `safedlete my-doctoral-thesis.doc` | Deletes the specified file (`my-doctoral-thesis.doc`). |