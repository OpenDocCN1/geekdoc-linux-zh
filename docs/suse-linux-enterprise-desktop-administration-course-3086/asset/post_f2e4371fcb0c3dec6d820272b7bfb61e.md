
18. Log out as root by entering

    exit

19. Close the terminal window.

## Objective 5—Work with Files and Directories

In this objective, you learn how to do the following to work with files:

- Copy, Move, and Rename Files and Directories
- Create Directories
- Delete Files and Directories
- Link Files

### Copy, Move, and Rename Files and Directories

To copy and move files and directories, you need to know how to do the following:

- Move and Rename Files with mv
- Copy Files with cp

#### Move and Rename Files with mv

You can use the mv (move) command to move one or more files to another directory, as in the following:

```bash
mv *.txt /tmp
```

You can also use the mv command to rename a file, as in the following:

```bash
mv recipe new_recipe
```

Table 7-15 shows options you can use with mv.

![](img/9129877170834ca9d5fdac5319bf5f12_228_0.png)

| Option | Description |
|---|---|
| `-i` | Asks for confirmation before moving or renaming a file. This prevents existing files with the same name from being overwritten. |
| `-u` | Only moves files that are newer than the target files of the same name. |

**Table 7-15**

#### Copy Files with cp

You can copy files and directories with the cp (copy) command. The syntax for using cp is:

```bash
cp source destination
```

When using the command cp, you need to remember the following:

- The command cp overwrites existing files without confirmation.
- You can avoid automatic overwriting by using the option `-i`. This option requires confirmation before overwriting occurs.
- If you want to copy just the contents of a directory (without the directory itself), the target directory must already exist. An example is making a backup copy of a directory using a different name.

For example, to copy the /tmp/quarterly-1/ directory with all of its subdirectories to the /tmp/expenses/ directory (which already exists), you would enter the following:

```bash
cp -R /tmp/quarterly-1/ /tmp/expenses
```

The result is a /tmp/expenses/quarterly-1/ directory.

To copy the contents of the proposals/ directory (all the files contained in it, including hidden files and subdirectories) to the proposals_old/ directory (this must already exist), you would enter the following:

```bash
geeko@da10:~ > ls -a proposals
. .. hidden quarterly-1 quarterly-2 quarterly-3
quarterly-4
geeko@da10:~ > cp -r proposals/. proposals_old
geeko@da10:~ > ls -a proposals_old
. .. hidden quarterly-1 quarterly-2 quarterly-3
quarterly-4
```

To avoid copying the hidden files, you would enter the following:

```bash
geeko@da10:~ > cp -r proposals/* proposals_old
geeko@da10:~ > ls -a proposals_old
. .. quarterly-1 quarterly-2 quarterly-3 quarterly-4
```

Table 7-16 shows the options you can use with cp.

| Option | Description |
|---|---|
| `-a, --archive` | Copies a directory and subdirectories (compare -R); symbolic links, file permissions, owners, and time stamps are not changed. |
| `--help` | Displays the options of cp. |
| `-i, --interactive` | Asks before overwriting. |
| `-R, -r, --recursive` | Copies directories recursively (the directory and any subdirectories). |
| `-s, --symbolic-link` | Creates symbolic links instead of copying. |
| `-l, --link` | Links files instead of copying them. |
| `-u, --update` | Copies a file only when the source file is newer than the destination file or when the destination file is missing. |

Table 7-16

## Create Directories

You can use the *mkdir* (*make directory*) command to create new directories (such as mkdir proposal). The option `-p` lets you create a complete path, as in the following:

```bash
mkdir -p proposal/january
```

## Delete Files and Directories

In this section, you learn how to do the following:

- Use `rmdir` to Delete Empty Directories
- Use `rm` to Delete Files and Directories

### Use rmdir to Delete Empty Directories

You can use the `rmdir` (*remove directory*) command to remove the indicated directory or directories (for example, rmdir proposal). The directory or directories must be empty before you can delete them.

### Use rm to Delete Files and Directories

You can use the `rm` (*remove*) command to delete files without being asked for confirmation, as in the following:

```bash
rm part*
```

This example deletes all files in the current directory that begin with **part**. If the user does not have sufficient permissions to delete a file, the file remains unchanged and an error message is displayed.

![](img/9129877170834ca9d5fdac5319bf5f12_230_0.png)

> Files deleted with the `rm` command cannot be restored.

Table 7-17 shows options you can use with `rm`.

| Option | Description |
|---|---|
| `-i` | Asks for confirmation before deleting. |
| `-r` | *(recursively)* Allows full directories to be deleted. |
| `-f` | *(force)* By default, `rm` asks for confirmation if the file that should be deleted is read-only. Use this option to delete files without being asked for confirmation. |

Table 7-17

![](img/9129877170834ca9d5fdac5319bf5f12_231_0.png)

## Exercise 7-4: Copy, Move, and Delete Files, Create and Delete Directories

In this exercise, copy and move files with the `cp` and `mv` commands, create new directories with the `mkdir` command, and delete files and directories with the `rm` and `rmdir` commands.

### Detailed Steps to Complete This Exercise

- Part I: Copy and Move Files and Directories
- Part II: Create New Directories
- Part III: Delete Files and Directories

### Part I: Copy and Move Files and Directories

To copy and move files and directories, do the following:

1. Open a terminal window.
2. Rename `new_file` (created in the exercise *Create and View Files*) to `my_file` by entering:
   ```bash
   mv new_file my_file
   ```
3. Verify that the file was renamed by entering:
   ```bash
   ls -l
   ```
4. Copy `my_file` by entering:
   ```bash
   cp my_file my_file1
   ```
5. Verify that `my_file1` was created by entering:
   ```bash
   ls -l my*
   ```
6. Copy the `/usr/bin/rename` and `/usr/bin/tac` files to the `/tmp` directory by entering:
   ```bash
   cp /usr/bin/rename /usr/bin/tac /tmp
   ```
7. Verify that the files were copied by entering:
   ```bash
   ls -l /tmp
   ```
8. Move the file `/tmp/tac` to the home directory by entering:
   ```bash
   mv /tmp/tac ~
   ```
9. Verify the move by entering:
   ```bash
   ls -l
   ```
10. Rename the `/tmp/rename` file to `~/my_file2` and move it by entering:
    ```bash
    mv /tmp/rename ~/my_file2
    ```
11. Verify that the file `my_file2` exists by entering:
    ```bash
    ls -l
    ```
12. Copy the complete /bin directory to the home directory with the new directory named my_dir by entering
    ```bash
    cp -r /bin ~/my_dir
    ```
13. Verify that the files were copied by entering
    ```bash
    ls -l ~/my_dir
    ```

### Part II: Create New Directories

To create new directories, do the following:

1. Create a directory named new_dir inside the my_dir directory by entering
    ```bash
    mkdir ~/my_dir/new_dir
    ```
2. Verify that the directory was created by entering
    ```bash
    ls ~/my_dir
    ```
3. Create a gecko_dir/empty_dir directory by entering
    ```bash
    mkdir -p ~/gecko_dir/empty_dir
    ```
4. Verify that gecko_dir was created by entering
    ```bash
    ls
    ```
5. Verify that empty_dir was created by entering
    ```bash
    ls gecko_dir
    ```
6. Close the terminal window.

### Part III: Delete Files and Directories

To delete files and directories, do the following:

1. Open a terminal window.
2. Try to remove the ~/gecko_dir directory by entering
    ```bash
    rmdir gecko_dir
    ```
    A message is displayed indicating that the directory cannot be removed because the directory is not empty.
3. Remove the ~/gecko_dir/empty_dir directory by entering
    ```bash
    rmdir gecko_dir/empty_dir
    ```
4. Verify that the /empty_dir directory has been removed by entering
    ```bash
    ls gecko_dir
    ```
5. Remove the ~/gecko_dir directory by entering
    ```bash
    rmdir gecko_dir
    ```
