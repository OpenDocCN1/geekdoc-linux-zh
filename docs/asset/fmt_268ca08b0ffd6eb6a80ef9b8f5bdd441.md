
```text
# mv /exam /test

# ls -lR /test
/test:
total 2
drwxr-xr-x  3 root     other       512 Apr 13 17:33 Solaris

/test/Solaris:
total 2
drwxr-xr-x  2 root     other       512 Apr 13 17:33 8
```

```text
/test/Solaris/8:
total 0
```

### 使用 rmdir 或 rm 命令删除目录

可以使用 `rmdir(1)` 或 `rm(1)` 命令来删除目录。`rmdir` 命令会删除以一个或多个命令行参数（以空格分隔）形式指定的目录。如果目录中包含文件或其他目录，则删除操作会失败。如果指定了 `-p` 命令行参数，则所有为空的父目录也会一并删除。`-s` 命令行参数用于抑制错误消息，如下例所示：

```text
# rmdir /test/Solaris/8
# ls -lR /test
/test:
total 2
drwxr-xr-x 2 root     other      512 Apr 13 19:15 Solaris

/test/Solaris:
total 0

# rmdir -p /test/Solaris

# ls -lR /test
/test: No such file or directory
#
```

`rm(1)` 命令同样可以删除一个或多个以命令行参数（以空格分隔）形式指定的目录。只有在指定了 `-R` 或 `-r` 命令行参数时，才能删除目录。这两个命令行参数都会递归地删除被删除目录*下*的所有文件和子目录。请注意，你可以使用 `rmdir` 命令删除父目录（即位于被删除目录*之上*的目录），如下例所示：

```text
# mkdir -p /test/Solaris/8

# rm /test
rm: /test is a directory

# rm -r /test

# ls -lR /test
/test: No such file or directory
#
```

`-i` 命令行参数可为删除命令提供交互式控制：

```text
# mkdir -p /test/Solaris/8

# rm -r -i /test
rm: examine files in directory /test (yes/no)? y
rm: examine files in directory /test/Solaris (yes/no)? y
rm: examine files in directory /test/Solaris/8 (yes/no)? y
rm: remove /test/Solaris/8/ (yes/no)? y
rm: remove /test/Solaris (yes/no)? y
rm: remove /test/ (yes/no)? y
#
```

通常情况下，如果 `rm` 命令遇到写保护的文件，它会提示确认是否删除该文件。但是，如果指定了 `-f` 命令行参数，则写保护的文件会在不确认的情况下被删除。`-f` 命令行参数不能与 `-i` 命令行参数同时指定。

### 文件

通常，系统程序和应用程序会创建文件。这些文件可以根据需要复制、移动（或重命名）和删除。这些操作由以下命令执行：

- `cp(1)` — 复制一个或多个文件。
- `mv(1)` — 移动或重命名文件。
- `rm(1)` — 删除一个或多个文件。

### 使用 cp 命令复制文件

`cp(1)` 命令将一个或多个文件复制到另一个目录，或以不同的名称创建现有文件的副本。请注意，当复制多个文件时，不能对它们进行重命名。

将一个或多个文件复制到另一个目录时，最后一个命令行参数是目标目录，前面所有的命令行参数是要复制的文件。要复制的文件可以是完整的文件名、使用元字符选择的多个文件，或它们的任意组合。多个文件名以空格分隔。在以下示例中，前两个 `cp` 命令将一个文件复制为不同的文件名。第三个命令将多个文件复制到另一个目录中：

```text
# ls -l
total 224
-rw-r--r--   1 root     other      103306 Apr 13 20:48 file1

# cp file1 file2

# ls -l
total 448
-rw-r--r--   1 root     other      103306 Apr 13 20:48 file1
-rw-r--r--   1 root     other      103306 Apr 13 20:48 file2

# cp file2 xfile

# ls -l
total 672
-rw-r--r-- 1 root other 103306 Apr 13 20:48 file1
-rw-r--r-- 1 root other 103306 Apr 13 20:48 file2
-rw-r--r-- 1 root other 103306 Apr 13 20:48 xfile

# cp xfile /tmp

# ls -l /tmp
total 1496
-rw------- 1 daemon other 19521 Apr 6 00:52 ab2.socat.cache
-rw-r--r-- 1 root other 103306 Apr 6 02:10 comp
-rw-r--r-- 1 root other 307892 Apr 4 18:57 dtdbcache_0
-rw-r--r-- 1 root other 103306 Apr 13 20:49 file1
-rw-r--r-- 1 root other 103306 Apr 13 20:49 file2
-rw-r--r-- 1 root other 5032 Apr 4 18:56 fs_data
-rw-r--r-- 1 root other 200 Apr 9 00:45 svsdtouchck390
-rw-r--r-- 1 root other 103306 Apr 13 20:49 xfile
#
```

### 使用 mv 命令移动和重命名文件

`mv(1)` 命令可用于：

- 将一个或多个文件移动到另一个目录。
- 在当前目录中重命名文件。
- 将文件移动到另一个目录并同时对其进行重命名。

在移动一个或多个文件时，最后一个命令行参数是目标目录，前面所有的命令行参数是要移动的文件。要移动的文件可以是完整的文件名、使用元字符选择的多个文件，或它们的任意组合。文件名必须以空格分隔，如下例所示：

```text
# ls -R /test
/test:
Solaris

/test/Solaris:
8

/test/Solaris/8:
310-011  310-012  sysadmin

# mv /test/Solaris/8/310-* /test/Solaris/8/sysadmin

# ls -R /test
/test:
Solaris

/test/Solaris:
8

/test/Solaris/8:
sysadmin

/test/Solaris/8/sysadmin:
310-011 310-012
```

单个文件可以在当前目录中重命名，也可以移动到另一个目录并同时重命名。在以下示例中，第一个 `mv` 命令将 310-011 文件重命名。第二个命令将其移动到另一个目录（父目录或 `..` 目录）。第三个命令将 310-012 文件移动到父目录并同时重命名：

```text
# ls
310-011  310-012

# mv 310-011 part1

# mv part1 ..

# mv 310-012 ../part2
#
```

### 使用 rm 命令删除文件

`rm(1)` 命令删除一个或多个以命令行参数形式指定的文件。要删除的文件可以是完整的文件名、使用元字符选择的多个文件，或它们的任意组合。多个文件名必须以空格分隔。`-i` 命令行参数可为删除命令提供交互式控制。通常情况下，如果 `rm` 命令遇到写保护的文件，它会提示确认是否删除该文件。但是，如果指定了 `-f` 命令行参数，则写保护的文件会在不确认的情况下被删除。`-f` 命令行参数不能与 `-i` 命令行参数同时指定，如下例所示：

```text
# ls
file1  file2  xfile

# rm xfile file*

# ls
#
```

![](img/b957f979417d9f16274c2eb52c8f2c9f_255_0.png)

以点字符开头（如 `.profile`）的文件和目录名，不会包含在使用元字符的多个文件/目录规范中。例如，`profile` 并不包含 `.profile`。以点开头的文件必须单独指定，并且需要在其前面加上一个点，如 `.*`。

## vi 编辑器
