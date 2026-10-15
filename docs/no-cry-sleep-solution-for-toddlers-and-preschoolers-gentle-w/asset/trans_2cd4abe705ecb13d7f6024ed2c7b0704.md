

| 命令 | 执行 |
|---|---|
| cp filename filename | 复制一个文件。cp 需要两个参数：原始文件和新副本的名称。你可以使用路径名将文件复制到不同目录：$ cp today reports/monday |
| cp -r dirname dirname | 将子目录从一个目录复制到另一个目录。被复制的目录包含其所有子目录：$ cp -r letters/thankyou oldletters |
| mv filename filename | 移动（重命名）一个文件。mv 需要两个参数：第一个是要移动的文件。第二个参数可以是新的文件名或目录的路径名。如果它是目录的名称，则文件会被 literally 移动到该目录，改变文件的路径名：$ mv today /home/chris/reports |
| mv dirname dirname | 移动目录。在这种情况下，第一个和最后一个参数都是目录：$ mv letters/thankyou oldletters |
| ln filename filename | 为文件创建额外的名称，称为链接。可以在一个目录中创建一个链接，引用另一个目录中的文件：$ ln today reports/monday |
| rm filenames | 删除（擦除）一个文件。可以接受任意数量的文件名作为参数。 literally 删除对文件的链接。如果一个文件有多个链接，你需要删除所有链接才能擦除文件：$ rm today weather weekend |

表 10-5 文件操作

## 链接：ln 命令

你可以使用 ln 命令为文件提供多个名称。你可能希望使用不同的文件名引用一个文件，以便从不同目录访问它。额外的名称通常称为链接。Linux 支持两种不同类型的链接，硬链接和符号链接。硬链接 literally 是同一文件的另一个名称，而符号链接则像引用另一个文件的快捷方式。符号链接更加灵活，可以在许多不同的文件系统上工作，而硬链接仅限于本地文件系统。此外，硬链接会引入安全问题，因为它允许从可能具有公共访问权限的链接直接访问你可能想要保护的原始文件。链接通常以符号链接的形式实现。

### 符号链接

要设置符号链接，你使用 ln 命令并带上 -s 选项和两个参数：原始文件的名称和新的附加文件名。ls 操作会列出两个文件名，但只会存在一个物理文件。

```
$ ln -s original-file-name added-file-name
```

在下一个示例中，today 文件被赋予了额外的名称 weather。它只是 today 文件的另一个名称。

```
$ ls
today
$ ln -s today weather
$ ls
today weather
```

你可以通过多次对同一文件使用 ln 命令来为同一文件提供多个名称。在下一个示例中，文件 today 被赋予了 weather 和 weekend 两个名称：

```
$ ln -s today weather
$ ln -s today weekend
$ ls
today weather weekend
```

如果你列出符号链接及其文件的完整信息，你会发现显示的信息是不同的。在下一个示例中，用户使用带 -l 选项的 ls 命令列出 lunch 和 /home/george/veglist 的完整信息。行中的第一个字符指定文件类型。符号链接有自己的文件类型，用 l 表示。lunch 的文件类型是 l，表示它是一个符号链接，而不是普通文件。术语“group”后面的数字是文件的大小。请注意大小不同。lunch 文件的大小只有 4 字节。这是因为 lunch 只是一个符号链接——一个保存另一个文件路径名的文件——而路径名只占用几个字节。它不是对 veglist 文件的直接硬链接。

```
$ ls lunch /home/george/veglist
lrw-rw-r-- 1 chris group 4 Feb 14 10:30 lunch
-rw-rw-r-- 1 george group 793 Feb 14 10:30 veglist
```

要擦除一个文件，你只需要删除其原始名称（以及对其的任何硬链接）。如果留下任何符号链接，它们将无法访问该文件。在这种情况下，符号链接将保存一个不再存在的文件的路径名。

### 硬链接

你可以通过多次对同一文件使用 ln 命令来为同一文件提供多个名称。要设置硬链接，你使用不带 -s 选项的 ln 命令和两个参数：原始文件的名称和新的附加文件名。ls 操作会列出两个文件名，但只会存在一个物理文件。

```
$ ln original-file-name added-file-name
```

在下一个示例中，monday 文件被赋予了额外的名称 storm。它只是 monday 文件的另一个名称。

```
$ ls
today
$ ln monday storm
$ ls
monday storm
```

