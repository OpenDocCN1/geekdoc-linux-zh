

### 5.4.1.2 更改目录权限

更改目录权限的过程与更改文件权限相同。但是，要列出目录的信息，需要使用 `ls -ld` 命令：

```text
$ ls -ld project
drwxr-xr-x  2 larry  system  32 Jun 5 10:07 project
$
```

现在使用 `chmod g+w` 命令更改权限，使组（g）对目录 project 具有写权限（+w）：

```text
$ chmod g+w project
$ ls -ld project
drwxrwxr-x  2 larry  system  32 Jun 5 10:07 project
$
```

### 5.4.1.3 使用模式匹配字符

如果要对目录中所有条目的权限进行相同的更改，可以将模式匹配字符（`*`）与 chmod 命令一起使用。有关模式匹配字符的信息，请参阅第 2 章。

在以下示例中，命令 `chmod g+x *` 为当前目录中的所有文件（*）授予组（g）执行（x）权限：

```text
$ chmod g+x *
$
```

现在输入 `ls -l` 命令，显示组现在对当前目录中的所有文件都具有执行（x）权限：

```text
$ ls -l
total 7
-rw-rwxrw-  1 larry  system  101 Jun 5 10:03 file1
-rw-r-xr--  1 larry  system  171 Jun 5 10:03 file2
-rw-r-xr--  1 larry  system  130 Jun 5 10:06 file3
drwxrwxr-x  2 larry  system   32 Jun 5 10:07 project
-rw-r-xr--  1 larry  system    0 Jun 5 11:03 record1
-rw-r-xr--  1 larry  system    0 Jun 5 11:03 record6
drwxr-xr-x  2 larry  system   32 Jun 5 10:31 reports
$
```

### 5.4.1.4 设置绝对权限

绝对权限赋值（=）会重置一个或多个文件的所有权限，无论这些权限之前是如何设置的。

在示例 5-1 中，`ls -l` 命令列出了 file3 文件的权限。然后，`chmod a=rwx` 命令为所有用户（a）赋予所有三种权限（rwx）。

**示例 5-1：设置绝对权限**

```text
$ ls -l file3
-rw-r-xr--  1 larry  system  130 Jun 5 10:06 file3
$ chmod a=rwx file3
$ ls -l file3
-rwxrwxrwx  1 larry  system  130 Jun 5 10:06 file3
$
```

你也可以使用绝对赋值来移除权限。在示例 5-2 中，`chmod a=rw file3` 命令从 file3 文件中移除了所有用户（a）的执行权限（x）：

**示例 5-2：移除绝对权限**

```text
$ chmod a=rw file3
$ ls -l file3
-rw-rw-rw-  1 larry  system  130 Jun 5 10:06 file3
$
```

### 5.4.2 使用八进制数指定权限

你也可以使用八进制数来更改文件和目录权限。

要使用八进制数权限代码与 chmod 命令，请输入以下形式的命令：

```text
chmod octalnumber filename
```

八进制数条目是一个 3 位八进制数，用于指定所有者、组和其他用户的权限。文件名条目是要更改权限的文件的名称。它可以是文件名，也可以是用空格分隔的文件名列表。你也可以使用模式匹配字符来指定文件。更多信息请参见第 5.4.1.3 节。

每种权限类型对应一个八进制数：

- 4 = 读
- 2 = 写
- 1 = 执行

要指定一组权限（权限字段），请将相应的八进制数相加（r、w 和 x 分别表示读、写和执行）：

```text
3 = -wx (2 + 1)
6 = rw- (4 + 2)
7 = rwx (4 + 2 + 1)
0 = --- (无权限)
```

表 5–2 列出了八种可能的权限组合。

**表 5–2：权限组合**

| 八进制数 | 二进制数 | 权限 | 说明 |
|---|---|---|---|
| 0 | 000 | None | 不授予任何权限 |
| 1 | 001 | --x | 执行 |
| 2 | 010 | -w- | 写 |
| 3 | 011 | -wx | 写/执行 |
| 4 | 100 | r-- | 读 |
| 5 | 101 | r-x | 读/执行 |
| 6 | 110 | rw- | 读/写 |
| 7 | 111 | rwx | 读/写/执行 |

文件或目录的完整权限代码由 3 位八进制数指定，每一位分别对应所有者、组和其他用户。表 5–3 显示了一些典型的权限代码及其与权限字段的关系。

**表 5–3：八进制数与权限字段的对应关系**

| 八进制数 | 所有者字段 | 组字段 | 其他用户字段 | 完整代码 |
|---|---|---|---|---|
| 777 | rwx | rwx | rwx | rwxrwxrwx |
| 755 | rwx | r-x | r-x | rwxr-xr-x |
| 700 | rwx | --- | --- | rwx------ |
| 666 | rw- | rw- | rw- | rw-rw-rw- |

例如，你可以使用以下命令通过八进制数更改 file3 的权限：

```text
$ ls -l file3
-rw-rw-rw-  1 larry  system  130 Jun 5 10:06 file3
$ chmod 754 file3
$ ls -l file3
```

