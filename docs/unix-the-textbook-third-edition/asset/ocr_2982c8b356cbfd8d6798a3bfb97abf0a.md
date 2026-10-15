![](bbox=[0.107, 0.091, 0.893, 0.201])

这里，**directory-names** 是要创建的目录的路径名。当你登录后，可以使用下面的命令在主目录中创建一个名为 **memos** 的子目录。新创建目录的访问权限由当前 umask 值决定（见 Chapter 5）。可以使用如下 `ls -ld memo` 命令确认目录是否创建成功：

```
```bash
$ mkdir memos
$ ls -ld memo
drwxr-xr-x 2 sarwar faculty 68 Aug 15 07:42 memo
$
```
```

同样，你也可以使用以下命令在 `/tmp` 目录中创建一个名为 **test_example** 的目录：

```
```bash
$ mkdir /tmp/test_example
$
```
```

在主目录中，你可以使用带有 `-p` 选项的 `mkdir` 命令创建 **professional** 目录及其子目录 **letters**，如下所示：

```
```bash
$ mkdir -p professional/letters
$
```
```

可以使用 `rmdir` 命令删除空目录。如果目录不为空，则必须先删除其中的文件和子目录，才能删除该目录。要删除非空目录，需要使用带有 `-r` 选项的 `rm` 命令（见 Chapter 6）。下面简要介绍 `rmdir` 命令。

![](bbox=[0.107, 0.696, 0.893, 0.828])

以下命令从当前工作目录中删除 **letters** 目录。如果 **letters** 不为空，`rmdir` 命令会显示错误信息：`rmdir: letters: Directory not empty`。如果 **letters** 是一个文件，命令会显示错误信息：`rmdir: letters: Not a directory.`