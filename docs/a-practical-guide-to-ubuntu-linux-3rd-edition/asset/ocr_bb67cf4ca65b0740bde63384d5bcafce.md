The `cp` command line in Figure 5–2 copies the file named **memo** to **memo.copy**. The period is part of the filename—just another character. The initial `ls` command shows that **memo** is the only file in the directory. After the `cp` command, a second `ls` shows two files in the directory, **memo** and **memo.copy**.

Sometimes it is useful to incorporate the date in the name of a copy of a file. The following example includes the date January 30 (**0130**) in the copied file:

```
$\ cp\ memo\ memo.0130$
```

Although it has no significance to Linux, the date can help you find a version of a file you created on a certain date. Including the date can also help you avoid overwriting existing files by providing a unique filename each day. For more information refer to “File names” on page 201.

Use `scp` (page 667) or `ftp` (page 687) when you need to copy a file from one system to another on a common network.

# **cp can destroy a file**

If the *destination-file* exists *before* you give a `cp` command, `cp` overwrites it. Because `cp` overwrites (and destroys the contents of) an existing *destination-file* without warning, you must take care not to cause `cp` to overwrite a file that you need. The `cp -i` (interactive) option prompts you before it overwrites a file. See page 139 for a tip on options.

The following example assumes that the file named **orange_2** exists before you give the `cp` command. The user answers **y** to overwrite the file:

```
$\ cp\ -i\ orange\ orange.2\
cp:\ overwrite\ ‘orange.2’?\ y$
```

# **MV: CHANGES THE NAME OF A FILE**

The `mv` (move) utility can rename a file without making a copy of it. The `mv` command line specifies an existing file and a new filename using the same syntax as `cp`:

```
$mv\ existing\-filename\ new\-filename$
```

The command line in Figure 5–3 changes the name of the file **memo** to **memo.0130**. The initial `ls` command shows that **memo** is the only file in the directory. After you give the `mv` command, **memo.0130** is the only file in the directory. Compare this result to that of the `cp` example in Figure 5–2.

The `mv` utility can be used for more than changing the name of a file. Refer to “mv, cp: Move or Copy Files” on page 212. See the `mv` info page for more information.

# **mv can destroy a file**

Just as `cp` can destroy a file, so can `mv`. Also like `cp`, `mv` has a `-i` (interactive) option. See the caution box labeled “cp can destroy a file.”