
> 在某些命令（如 `rm` 和 `cp`）中，`-r` 和 `-R` 选项具有相同的含义（递归）。
> 
> 如果你不确定要递归删除的目录中存在哪些文件，那么 `rm` 命令的 `-r` 选项是非常危险的。因此，`rm` 命令的 `-r` 选项通常被称为 `-recursive` 选项；如果你使用错误，可能需要准备简历。

# 第 5 章 Linux 文件系统管理

需要注意的是，上述文件管理命令被 Linux 用户、开发者和管理员经常使用。表 5-2 显示了常用文件管理命令的总结。

## 5-2 常见的 Linux 文件管理命令

| 命令 | 说明 |
| :--- | :--- |
| `mkdir` | 创建目录 |
| `rdir` | 删除空目录 |
| `mv` | 移动/重命名文件和目录 |
| `cp` | 复制包含文件的文件和目录（使用 `-r` 选项） |
| `alias` | 显示 BASH 别名 |
| `rm` | 删除包含文件的文件和目录（使用 `-r` 选项） |

### 查找文件

在使用上一节提到的文件管理命令之前，你必须知道所相关文件的位置。在 Linux 目录树中搜索文件的最快方法是使用 `locate` 命令，它是 `locate`（或 `secure`）命令的快捷方式。例如，要查看根目录下所有文件名包含“initab”一词的文件，只需在命令提示符输入 `locate initab`，将产生以下输出：

```
[root@server1]# locate initab

/usr/share/terminfo/a/ansi-inittabs

/usr/share/vim/vim2/syntax/initab.vim

/usr/share/man/ja/man5/initab.vim

/usr/share/man/en5/initab.gz

/usr/share/man/fr5/initab.gz

/usr/share/man/it5/initab.gz

/usr/share/man/ko5/initab.gz

[root@server1]# locate initab
```

## 管理文件和目录

`rm`（删除）命令接受一个参数列表，用于指定要删除文件的绝对路径或相对路径。与大多数命令一样，可以使用通配符来简化多个要删除的文件。一旦文件从文件系统中被删除，它将无法恢复。因此，在 Red Hat Linux 中，`rm` 命令被别名为带有 `-i` 选项的 `rm` 命令，它会交互式地提示用户选择是否继续删除。与 `cp` 命令一样，`rm` 命令也接受 `-f` 选项来覆盖此设置并立即删除文件。下面的示例演示了使用 `rm` 和 `rm -f` 命令删除当前目录和 `hosts2`：

```
[root@server1]# ls -F

current@Desktop/ hosts2 myprogram* myscript2* proj_files/

[root@server1]# rm current

rm: '?' y

[root@server1]# rm -f hosts2

[root@server1]# ls -F

Desktop/ myprogram* myscript2* proj_files/

[root@server1]# _
```

要删除目录，你可以使用 `rmdir`（删除目录）命令，但它仅在目录不包含文件时才能删除。要删除目录及其内部的文件，必须使用 `rm` 命令并指定要删除的是目录文件。记住之前提到的，在用 `cp` 命令时需要使用递归选项（`-r`）来复制目录；要删除一个完整的文件目录，你也可以在 `rm` 命令中使用递归选项（`-r`）。例如，如果 root 用户想要删除 `proj_files` 子目录及其内部的所有文件，而无需在每个文件删除时进行确认，她必须像下面的示例所示使用 `rm -rf proj_files`：

```
[root@server1]# ls -F

Desktop/ myprogram* proj_files/

[root@server1]# rmdir proj_files

rmdir: 'proj_files': Directory not empty

[root@server1]# rm -rf proj_files

[root@server1]# ls -F

Desktop/ myprogram* myscript2*

[root@server1]# _
```

> 在某些命令（如 `rm` 和 `cp`）中，`-r` 和 `-R` 选项具有相同的含义（递归）。
> 
> 如果你不确定要递归删除的目录中存在哪些文件，那么 `rm` 命令的 `-r` 选项是非常危险的。因此，`rm` 命令的 `-r` 选项通常被称为 `-recursive` 选项；如果你使用错误，可能需要准备简历。
