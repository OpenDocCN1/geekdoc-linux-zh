
如果你尝试合并一个文件或多个文件导致一个或多个文件不存在，`cat` 将合并所有可用文件，并在最后生成关于不存在文件的信息。如果你想合并两个文件 `testfile` 和 `testfile2` 到当前目录下的 `testfile`，而在执行以下命令时将 `testfile2` 误打为 `testfile`：

```
cat testfile testfile > testfile
```

你将得到类似的消息，且 `testfile` 只有 `testfile` 的内容：

```
cat: cannot open testfile
```

如果你使用 `-q` 标志，你将不会得到错误信息。

如果当前目录下的 `testfile` 包含以下行（注意最后一行包含特殊字符），`cat` 将显示：

```
This is a test file

This does not contain anything meaningful

This is for demo only

^F^F^F^F^F
```

如果你带有 `-n` 标志执行命令，`cat` 将显示带行号的行，但带有特殊字符的最后一行将显示为空行：

```
cat -n testfile
1 This is a test file
2
3 file does not contain anything meaningful
4 This is for demo only
5
```

如果你想确保显示的空行实际上不包含除不可打印字符以外的字符，请配合 `cat` 命令使用 `-v` 标志。这确保了不可打印字符被显示为打印字符：

```
cat -v testfile
This is a test file
This does not contain anything meaningful
This is for demo only
^F^F^F^F^F
```

`rcp`

到目前为止，我们有很多在本地主机目录之间移动或复制文件的命令。如果你需要从一个主机复制文件到另一个主机，可以使用 `rcp` 命令在不同或相同的主机之间复制文件。你可以在本地主机执行 `rcp` 命令在本地主机与远程主机或两个远程主机之间复制文件。

远程主机上的文件名由 `主机主机:目录/文件名` 指定。冒号 `(:)` 用作主机名和文件名之间的分隔符。

也可以通过 `username@hostname:/dirname/filename` 指定远程主机上的用户名。`@` 符号用作用户名和主机之间的分隔符。然而，用户名是可选的。如果不指定，远程主机上的用户名将与本地主机的用户相同。

如果源文件或目标文件都没有指定主机，`rcp` 命令的行为与 `cp` 命令相同。

如果远程主机上的文件名没有完全限定（即不是从根目录开始），则文件名或目录名被认为是从远程用户的家目录开始。

如果文件在远程主机上不存在，将以远程用户的默认权限创建。如果文件在远程主机上已存在，则保留目标文件的权限。

与 `cp` 命令一样，你可以使用 `rcp` 命令复制目录以及目录内的文件。

以下是可以使用 `rcp` 命令的一些标志位：

- `-p`：在创建目标文件时，保留源文件的修改日期、时间以及源文件的权限。
- `-r`：在复制目录时递归复制文件。

> 注意：若要使用 `rcp` 命令将文件传输到远程主机，你必须在远程主机的 `/etc/hosts.equiv` 文件中定义本地主机名，或者在远程用户家目录下的 `.hosts` 文件中定义本地主机名和用户名。

示例：如果你想将当前目录下的 `testfile` 复制到远程主机 `otherhost` 家目录下的 `testdir` 目录中的 `testfile`，请执行以下命令：

```
rcp testfile otherhost:testdir/testfile
```

如果本地主机的用户是 `tester`，则该命令将假设远程主机上的用户名也是 `tester`。如果远程主机上不存在 `testuser` 用户，且你必须在远程主机上使用用户名 `newtester`，请执行以下命令：

```
rcp testfile newtester@otherhost:testdir/testfile
```

如果你必须将 `testfile` 从远程主机 `otherhost1` 传输到另一个远程主机 `otherhost2`，并希望保留修改日期和权限，请执行以下命令：

```
rcp -p tester1@otherhost1:testfile tester2@otherhost2:testfile
```

这会将 `test` 从远程主机 `otherhost1` 上用户 `tester1` 的家目录复制到远程主机 `otherhost2` 上 `tester2` 的家目录。

如果你想从远程主机 `otherhost` 将 `/u/tester/testdir` 目录下的所有文件复制到本地主机的当前目录，请执行以下命令：

```
rcp testuser@otherhost:/u/testuser/testdir/*
```

这不会复制你在 `testdir` 中的任何子目录或子目录下的任何文件。要复制所有子目录及其内部文件，请使用以下命令：

```
rcp -r testuser@otherhost:/u/testuser/testdir/*
```

## ln

有时你需要为同一个文件提供备别名。这可以通过 `ln` 命令将一个文件名链接到另一个文件名来实现。你可以将文件链接到同一目录下的另一个名称，或者另一个目录下的同名文件。

将文件名链接到另一个文件名时，你只需要指定两个参数：源文件名和目标文件名。将文件名链接到目录时，你可以指定多个要链接到同一目录的文件名。

如果你使用硬链接（hard links），无法链接另一个文件系统的文件；但使用软链接（soft links），你可以跨不同的文件系统链接文件名。

`ln` 命令使用的标志位如下：

- `-s`：创建一个指向另一个文件或目录的软链接。在软链接中，链接文件包含原始文件的名称。当对链接文件进行操作时，将使用链接中的原始文件名来引用原始文件。
- `-f`：如果目标文件名已存在，则确保用链接文件名替换它。

默认情况下，`ln` 命令创建硬链接。

示例：如果你想将当前目录下的 `testfile` 链接到 `test2`，请执行以下命令：

```
ln testfile test2
```

这会创建一个链接到 `testfile` 的硬链接 `test2`。在这种情况下，如果删除了其中一个文件，另一个将保持不变。

如果 `testfile` 在当前目录中，且要将其链接到 `/u/testuser/testdir` 目录下的 `testfile`，请执行以下命令：

```
ln testfile /u/testuser/testdir
```

若要在当前目录下创建 `testfile1` 的符号链接，请执行以下命令：

```
ln -s testfile test2
```

这会创建一个链接 `testfile2`，它包含 `testfile1` 的名称。如果你删除了 `testfile1`，将留下一个指向空路径的孤立链接 `testfile2`（orphan link）。

如果你想将当前目录下的所有文件链接到另一个目录 `/u/testuser/testdir`，请执行以下命令：

```
ln * /u/testuer/testdir/
```

## 目录操作命令

在 UNIX 操作系统中设置用户用户时，通常会将 `/u/username` 设置为家目录。为了组织文件，你必须根据喜好建立目录。这里我们将介绍创建和删除目录的命令。

`mkdir`

要创建目录，使用 `mkdir` 命令。`mkdir` 命令接受多个名称。以下是 `mkdir` 命令的标志位：

- `-p`：如果父目录不存在，则创建它们。
- `-m`：指定目录的权限。

示例：如果你想在当前目录下创建一个目录 `testdir`，请执行以下命令：

```
mkdir testdir
```

如果你想在 `/u/testuser/testdir` 目录下创建一个目录 `testdir`，请执行以下命令：

```bash
mkdir /u/testuser/testdir
```

如果你想同时创建多个目录 `test1` 和 `test2`，请执行以下命令：

```bash
mkdir test1 test2
```

如果你想创建一个指定权限为 `755` 的目录 `testdir`，请执行以下命令：

```bash
mkdir -m 755 testdir
```

如果你想创建一个嵌套目录结构 `/u/user/testdir/subdir`，且父目录不存在，请执行以下命令：

```bash
mkdir -p /u/user/testdir/subdir
```

要删除目录，使用 `rmdir` 命令。`rmdir` 命令只有在目录为空（即其所有文件和目录都已删除）时才能删除。你可以指定多个目录名称作为参数。

- `-p`：删除指定路径下的所有目录。

示例：如果你想删除当前目录下的 `testdir`，请执行以下命令：

```bash
rmdir testdir
```

如果你想删除 `/u/testuser/testdir` 目录下的 `testdir`，请执行以下命令：

```bash
rmdir /u/testuser/testdir
```

如果你想同时删除目录 `test1` 和 `test2`，请执行以下命令：

```bash
rmdir test1 test2
```

如果你想删除一个嵌套目录结构 `/u/user/testdir/subdir`，且所有目录都为空，请执行以下命令：

```bash
rmdir -p /u/user/testdir/subdir
```
